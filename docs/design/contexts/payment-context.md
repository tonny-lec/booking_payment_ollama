---
doc_type: "context"
id: "payment-ctx-01"
bounded_context: "Payment"
status: "draft"
---

# 1. 目的
Paymentコンテキストは、ユーザーがサービスに対して支払いを行うための境界コンテキストです。このコンテキストは、支払いの作成、処理、キャンセルを管理し、冪等性を保証する機能を提供します。

# 2. 用語
- **支払い（Payment）**: ユーザーがサービスに対して支払う金額
- **冪等性（Idempotency）**: 同じ操作を複数回実行しても結果が同じになる性質
- **トランザクション（Transaction）**: 支払い処理の単位
- **ステータス（Status）**: 支払いの現在の状態（処理中、完了、失敗、キャンセル）

# 3. 集約一覧（Aggregate Catalog）
- **PaymentAggregate**: 支払いの作成、処理、キャンセルを管理
- **TransactionAggregate**: 支払いトランザクションを管理
- **StatusAggregate**: 支払いのステータス変更を管理

# 4. Context Map
```
[User] --(creates)--> [Payment]
[Payment] --(processes)--> [Transaction]
[Payment] --(updates)--> [Status]
[Payment] --(issues)--> [PaymentCreatedEvent]
```

# 5. 永続化
- 支払い情報: PostgreSQL
- トランザクション情報: PostgreSQL
- ステータス情報: PostgreSQL

# 6. ドメインイベント
- `PaymentCreatedEvent`: 支払い作成時
- `PaymentProcessedEvent`: 支払い処理時
- `PaymentCancelledEvent`: 支払いキャンセル時
- `PaymentFailedEvent`: 支払い失敗時

# 7. 非機能（SLO/Obs/Sec）
- **SLO**: 支払いAPIの可用性99.9%
- **Obs**: 全支払い操作のトレースとメトリクス収集
- **Sec**: 支払い情報の暗号化、冪等性の保証、再試行処理の実装

# 8. ADRリンク
- [ADR-005: 支払い冪等性の実装](../adr/005-idempotency-implementation.md)
- [ADR-006: 支払いステータス管理](../adr/006-payment-status-management.md)

# 9. Evidence（根拠：差分/ログ/計測/仕様）
- 支払いAPIの設計は、冪等性を保証するためのユニークIDと状態管理を実装
- パフォーマンス要件は、支払いリクエストの平均応答時間300ms以内

# 10. 未決事項
- 支払いの自動再試行処理
- 支払い失敗時のロールバック処理
- 顧客情報のセキュリティ対応