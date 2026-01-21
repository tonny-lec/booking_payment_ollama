---
doc_type: "usecase"
id: "booking-uc-01"
bounded_context: "Booking"
related_features: []
related_skills: []
status: "draft"
---

# 1. 目的 / 背景
Bookingコンテキストの予約作成機能は、ユーザーがサービスまたはリソースを予約できるようにするためのユースケースです。このユースケースでは、予約の作成、衝突の検出、状態の管理を定義します。

# 2. ユビキタス言語
- **予約（Booking）**: ユーザーが特定のサービスまたはリソースを予約すること
- **衝突（Conflict）**: 同じリソースに対して複数の予約が行われる状態
- **スロット（Slot）**: 予約可能な時間またはリソースの単位
- **状態遷移（State Transition）**: 予約のライフサイクルにおける状態変更

# 3. 依存関係（Context Map）
```
[User] --(creates)--> [Booking-Create]
[Booking-Create] --(checks)--> [Slot]
[Booking-Create] --(detects)--> [Conflict]
[Booking-Create] --(issues)--> [BookingCreatedEvent]
```

# 4. 入出力（Command/Query/Event）
## 入力（Command）
- `CreateBookingCommand`: 予約作成リクエスト
  - パラメータ: userId, resourceId, startTime, endTime

## 出力（Event）
- `BookingCreatedEvent`: 予約作成成功時
  - パラメータ: bookingId, userId, resourceId, startTime, endTime, status

# 5. ドメインモデル（集約/不変条件）
- **BookingAggregate**: 予約の作成、変更、キャンセルを管理
  - 不変条件: 予約は一意のIDを持ち、重複予約は許可されない

- **SlotAggregate**: 予約可能な時間またはリソースのスロットを管理
  - 不変条件: スロットは時間重複を防ぐためにロック機構が必要

- **ConflictAggregate**: 予約の衝突を検出および管理
  - 不変条件: 衝突は排他的ロックで処理される

# 6. API（OpenAPI参照）
API仕様は `docs/api/openapi/booking.yaml` で定義

# 7. 永続化
- 予約情報: PostgreSQL
- スロット情報: PostgreSQL
- 衝突情報: PostgreSQL

# 8. 失敗モードとリカバリ（timeout/retry/idempotency）
- **タイムアウト**: 予約作成リクエストがタイムアウトした場合、エラーを返す
- **再試行**: ネットワークエラーなどによる一時的な失敗は再試行可能
- **冪等性**: 同じ予約リクエストを複数回実行しても結果は同じ（IDempotent）

# 9. 観測性（logs/metrics/traces）
- 全予約作成リクエストのトレースIDを記録
- 予約作成成功/失敗のメトリクスを収集
- ログに予約作成リクエストの詳細を記録
- 衝突検出時のログを記録

# 10. セキュリティ（authn/authz/audit/PII）
- 予約情報のアクセス制御を実装
- 重要な操作は監査ログに記録
- PII（個人識別情報）は最小限に抑える

# 11. テスト戦略（Unit/Integration/Contract/E2E）
- **ユニットテスト**: 予約作成ロジックのテスト
- **統合テスト**: 予約情報とスロット情報の結合テスト
- **契約テスト**: OpenAPI仕様との整合性チェック
- **E2Eテスト**: 実際の予約フローのテスト

# 12. ADRリンク
- [ADR-003: 予約衝突防止の実装](../adr/003-conflict-prevention.md)
- [ADR-004: 予約状態管理](../adr/004-booking-state-management.md)

# 13. Evidence（根拠：差分/ログ/計測/仕様）
- 予約作成APIの設計は、同時実行制御とロック機構を用いて衝突を防止
- パフォーマンス要件は、予約作成リクエストの平均応答時間200ms以内

# 14. 未決事項
- 予約変更時の衝突処理方法
- キャンセル時のスロット再利用方法
- 予約の自動期限切れ処理