---
doc_type: "context"
id: "booking-ctx-01"
bounded_context: "Booking"
status: "draft"
---

# 1. 目的
Bookingコンテキストは、ユーザーがサービスまたはリソースを予約できるようにするための境界コンテキストです。このコンテキストは、予約の作成、衝突の検出、状態の管理を担当します。

# 2. 用語
- **予約（Booking）**: ユーザーが特定のサービスまたはリソースを予約すること
- **衝突（Conflict）**: 同じリソースに対して複数の予約が行われる状態
- **スロット（Slot）**: 予約可能な時間またはリソースの単位
- **状態遷移（State Transition）**: 予約のライフサイクルにおける状態変更

# 3. 集約一覧（Aggregate Catalog）
- **BookingAggregate**: 予約の作成、変更、キャンセルを管理
- **SlotAggregate**: 予約可能な時間またはリソースのスロットを管理
- **ConflictAggregate**: 予約の衝突を検出および管理

# 4. Context Map
```
[User] --(creates)--> [Booking-Create]
[Booking-Create] --(checks)--> [Slot]
[Booking-Create] --(detects)--> [Conflict]
[Booking-Create] --(issues)--> [BookingCreatedEvent]
```

# 5. 永続化
- 予約情報: PostgreSQL
- スロット情報: PostgreSQL
- 衝突情報: PostgreSQL

# 6. ドメインイベント
- `BookingCreatedEvent`: 予約作成成功時
- `BookingUpdatedEvent`: 予約更新時
- `BookingCancelledEvent`: 予約キャンセル時
- `ConflictDetectedEvent`: 衝突検出時

# 7. 非機能（SLO/Obs/Sec）
- **SLO**: 予約作成APIの可用性99.9%
- **Obs**: 全予約作成リクエストのトレースとメトリクス収集
- **Sec**: 予約情報のアクセス制御、重要な操作は監査ログに記録

# 8. ADRリンク
- [ADR-003: 予約衝突防止の実装](../adr/003-conflict-prevention.md)
- [ADR-004: 予約状態管理](../adr/004-booking-state-management.md)

# 9. Evidence（根拠：差分/ログ/計測/仕様）
- 予約作成APIの設計は、同時実行制御とロック機構を用いて衝突を防止
- パフォーマンス要件は、予約作成リクエストの平均応答時間200ms以内

# 10. 未決事項
- 予約変更時の衝突処理方法
- キャンセル時のスロット再利用方法
- 予約の自動期限切れ処理