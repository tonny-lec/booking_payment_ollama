---
doc_type: "usecase"
id: "payment-uc-02"
bounded_context: "Payment"
related_features: []
related_skills: []
status: "draft"
---

# 1. 目的 / 背景
Paymentコンテキストの支払い作成機能は、ユーザーがサービスに対して支払いを行うためのユースケースです。このユースケースでは、支払いの作成、処理、冪等性の保証を定義します。

# 2. ユビキタス言語
- **支払い（Payment）**: ユーザーがサービスに対して支払う金額
- **冪等性（Idempotency）**: 同じ操作を複数回実行しても結果が同じになる性質
- **トランザクション（Transaction）**: 支払い処理の単位
- **ステータス（Status）**: 支払いの現在の状態（処理中、完了、失敗、キャンセル）

# 3. 依存関係（Context Map）
```
[User] --(creates)--> [Payment-Create]
[Payment-Create] --(processes)--> [Transaction]
[Payment-Create] --(updates)--> [Status]
[Payment-Create] --(issues)--> [PaymentCreatedEvent]
```

# 4. 入出力（Command/Query/Event）
## 入力（Command）
- `CreatePaymentCommand`: 支払い作成リクエスト
  - パラメータ: userId, amount, currency, orderId, paymentMethod

## 出力（Event）
- `PaymentCreatedEvent`: 支払い作成成功時
  - パラメータ: paymentId, userId, amount, currency, orderId, status, timestamp
- `PaymentProcessedEvent`: 支払い処理完了時
  - パラメータ: paymentId, status, transactionId, processedAt
- `PaymentFailedEvent`: 支払い失敗時
  - パラメータ: paymentId, status, errorMessage, failedAt

# 5. ドメインモデル（集約/不変条件）
- **PaymentAggregate**: 支払いの作成、処理、キャンセルを管理
  - 不変条件: 支払いは一意のIDを持ち、冪等性を保証

- **TransactionAggregate**: 支払いトランザクションを管理
  - 不変条件: トランザクションは一意のIDを持ち、処理は原子性を保証

- **StatusAggregate**: 支払いのステータス変更を管理
  - 不変条件: ステータス変更は履歴を保持し、一貫性を保つ

# 6. API（OpenAPI参照）
API仕様は `docs/api/openapi/payment.yaml` で定義

# 7. 永続化
- 支払い情報: PostgreSQL
- トランザクション情報: PostgreSQL
- ステータス情報: PostgreSQL

# 8. 失敗モードとリカバリ（timeout/retry/idempotency）
- **タイムアウト**: 支払いリクエストがタイムアウトした場合、エラーを返す
- **再試行**: ネットワークエラーなどによる一時的な失敗は再試行可能
- **冪等性**: 同じ支払いリクエストを複数回実行しても結果は同じ

# 9. 観測性（logs/metrics/traces）
- 全支払いリクエストのトレースIDを記録
- 支払い成功/失敗のメトリクスを収集
- ログに支払いリクエストの詳細を記録
- 支払いステータス変更の履歴を記録

# 10. セキュリティ（authn/authz/audit/PII）
- 支払い情報の暗号化を実装
- 重要な操作は監査ログに記録
- PII（個人識別情報）は最小限に抑える
- 支払い処理は安全な通信プロトコルを使用

# 11. テスト戦略（Unit/Integration/Contract/E2E）
- **ユニットテスト**: 支払い作成ロジックのテスト
- **統合テスト**: 支払い情報とトランザクション情報の結合テスト
- **契約テスト**: OpenAPI仕様との整合性チェック
- **E2Eテスト**: 実際の支払いフローのテスト

# 12. ADRリンク
- [ADR-005: 支払い冪等性の実装](../adr/005-idempotency-implementation.md)
- [ADR-006: 支払いステータス管理](../adr/006-payment-status-management.md)

# 13. Evidence（根拠：差分/ログ/計測/仕様）
- 支払いAPIの設計は、冪等性を保証するためのユニークIDと状態管理を実装
- パフォーマンス要件は、支払いリクエストの平均応答時間300ms以内

# 14. 未決事項
- 支払いの自動再試行処理
- 支払い失敗時のロールバック処理
- 顧客情報のセキュリティ対応