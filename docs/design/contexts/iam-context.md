---
doc_type: "context"
id: "iam-ctx-01"
bounded_context: "IAM"
status: "draft"
---

# 1. 目的
IAM（Identity and Access Management）コンテキストは、システム内のユーザー認証と認可を管理するための境界コンテキストです。このコンテキストは、ユーザーの認証情報の管理、アクセス権限の付与、セキュリティトークンの発行と検証を行うことを目的としています。

# 2. 用語
- **ユーザー（User）**: システムにアクセスする個人またはサービス
- **認証（Authentication）**: ユーザーがシステムにアクセスできるかどうかを確認するプロセス
- **認可（Authorization）**: 認証されたユーザーが特定のリソースにアクセスできるかどうかを決定するプロセス
- **トークン（Token）**: 認証されたユーザーを識別するために使用される情報
- **セッション（Session）**: ユーザーがシステムにアクセスしている期間

# 3. 集約一覧（Aggregate Catalog）
- **UserAggregate**: ユーザーの基本情報と認証情報を管理
- **TokenAggregate**: トークンの発行、検証、無効化を管理
- **SessionAggregate**: ユーザーのセッション情報を管理

# 4. Context Map
```
[User] --(uses)--> [IAM]
[IAM] --(authenticates)--> [User]
[IAM] --(issues)--> [Token]
```

# 5. 永続化
- ユーザー情報: PostgreSQL
- トークン情報: Redis（短期間の有効期限付き）
- セッション情報: PostgreSQL

# 6. ドメインイベント
- `UserAuthenticatedEvent`: ユーザー認証成功時
- `TokenIssuedEvent`: トークン発行時
- `SessionCreatedEvent`: セッション作成時
- `UserLoggedOutEvent`: ユーザーがログアウト時

# 7. 非機能（SLO/Obs/Sec）
- **SLO**: 認証APIの可用性99.9%
- **Obs**: 全認証リクエストのトレースとメトリクス収集
- **Sec**: JWTトークンの暗号化、パスワードはハッシュ化、セッション管理のセキュリティ

# 8. ADRリンク
- [ADR-001: JWTトークンの使用](../adr/001-jwt-token-usage.md)
- [ADR-002: パスワードハッシュ化](../adr/002-password-hashing.md)

# 9. Evidence（根拠：差分/ログ/計測/仕様）
- 認証APIの設計は、OAuth 2.0とJWTの標準を参照
- セキュリティ要件は、OWASP Top 10に準拠
- パフォーマンス要件は、認証リクエストの平均応答時間100ms以内

# 10. 未決事項
- トークンの再発行処理の実装方法
- ログアウト時のセッション無効化の実装方法
- 多要素認証（MFA）の実装計画