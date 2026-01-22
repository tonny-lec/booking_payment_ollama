---
doc_type: "usecase"
id: "iam-uc-01"
bounded_context: "IAM"
related_features: []
related_skills: []
status: "draft"
---

# 1. 目的 / 背景
IAMコンテキストのログイン機能は、ユーザーがシステムに認証されるためのユースケースです。このユースケースでは、ユーザーの認証情報の検証、トークンの発行、セッションの管理を定義します。

# 2. ユビキタス言語
- **ユーザー（User）**: システムにアクセスする個人またはサービス
- **認証（Authentication）**: ユーザーがシステムにアクセスできるかどうかを確認するプロセス
- **トークン（Token）**: 認証されたユーザーを識別するために使用される情報
- **セッション（Session）**: ユーザーがシステムにアクセスしている期間

# 3. 依存関係（Context Map）
```
[User] --(authenticates)--> [IAM-Login]
[IAM-Login] --(verifies)--> [User]
[IAM-Login] --(issues)--> [Token]
```

# 4. 入出力（Command/Query/Event）
## 入力（Command）
- `LoginCommand`: ログインリクエスト
  - パラメータ: username, password

## 出力（Event）
- `UserAuthenticatedEvent`: ユーザー認証成功時
  - パラメータ: userId, username, timestamp
- `TokenIssuedEvent`: トークン発行時
  - パラメータ: userId, token, expiryTime

# 5. ドメインモデル（集約/不変条件）
- **UserAggregate**: ユーザーの認証情報を管理
  - 不変条件: ユーザー名は一意、パスワードはハッシュ化

- **TokenAggregate**: トークンの発行、検証、無効化を管理
  - 不変条件: トークンは有効期限付き、再発行可能

- **SessionAggregate**: ユーザーのセッション情報を管理
  - 不変条件: セッションは一意のIDを持ち、期限付き

# 6. API（OpenAPI参照）
API仕様は `docs/api/openapi/iam.yaml` で定義

# 7. 永続化
- ユーザー情報: PostgreSQL
- トークン情報: Redis（短期間の有効期限付き）
- セッション情報: PostgreSQL

# 8. 失敗モードとリカバリ（timeout/retry/idempotency）
- **タイムアウト**: 認証リクエストがタイムアウトした場合、エラーを返す
- **再試行**: ネットワークエラーなどによる一時的な失敗は再試行可能
- **冪等性**: 同じログインリクエストを複数回実行しても結果は同じ（認証状態が変化しない）

# 9. 観測性（logs/metrics/traces）
- 全ログインリクエストのトレースIDを記録
- ログイン成功/失敗のメトリクスを収集
- ログにログインリクエストの詳細を記録
- 認証失敗時のログを記録

# 10. セキュリティ（authn/authz/audit/PII）
- パスワードはハッシュ化して保存
- JWTトークンの暗号化を実装
- 重要な操作は監査ログに記録
- PII（個人識別情報）は最小限に抑える
- 認証処理は安全な通信プロトコルを使用

# 11. テスト戦略（Unit/Integration/Contract/E2E）
- **ユニットテスト**: ログインロジックのテスト
- **統合テスト**: ユーザー情報とトークン情報の結合テスト
- **契約テスト**: OpenAPI仕様との整合性チェック
- **E2Eテスト**: 実際のログインフローのテスト

# 12. ADRリンク
- [ADR-001: JWTトークンの使用](../adr/001-jwt-token-usage.md)
- [ADR-002: パスワードハッシュ化](../adr/002-password-hashing.md)

# 13. Evidence（根拠：差分/ログ/計測/仕様）
- ログインAPIの設計は、OAuth 2.0とJWTの標準を参照
- セキュリティ要件は、OWASP Top 10に準拠
- パフォーマンス要件は、認証リクエストの平均応答時間100ms以内

# 14. 未決事項
- トークンの再発行処理の実装方法
- ログアウト時のセッション無効化の実装方法
- 多要素認証（MFA）の実装計画