# Tomario

ホテルの客室予約システム「Tomario」のAWSインフラポートフォリオ、各リポジトリへの入り口となるトップページです。

Terraform + GitHub Actions でAWSインフラをコードで管理しています。
dev（開発）・staging（負荷試験・障害試験）・production（本番）の3環境をAWSアカウント分離し、staging で検証した構成をそのまま production に適用しています。

## ディレクトリ構成

```
Tomario（ポートフォリオ全体）
├── tomario-infra/        … Terraformによるインフラ管理
│   ├── envs/              … 環境別コード（nonprod/dev,staging,shared・prod/production）
│   ├── modules/            … network/backend/database/frontend/security/monitoring/cost/ecr/logging
│   ├── bootstrap-nonprod/  … nonprodアカウントのOIDC/IAM初期セットアップ
│   ├── bootstrap-prod/     … prodアカウントのOIDC/IAM初期セットアップ
│   └── docs/                … アーキテクチャ構成図
├── tomario-app/          … Flask API + 静的フロントエンド
└── tomario-docs/         … 設計ドキュメント
    ├── requirements/          … 要件定義書
    ├── basic-design/          … 基本設計書
    └── environment-definitions/ … 環境定義書
```

## リポジトリ

| リポジトリ | 内容 |
|---|---|
| [tomario-infra](https://github.com/Tomario-portfolio/tomario-infra) | Terraformによるインフラ管理（9モジュール構成、nonprod/prodアカウント分離） |
| [tomario-app](https://github.com/Tomario-portfolio/tomario-app) | Flask API + 静的フロントエンド |
| [tomario-docs](https://github.com/Tomario-portfolio/tomario-docs) | 要件定義書・基本設計書・環境定義書 |
