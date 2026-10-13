# Tomario

ホテルの客室予約システム「Tomario」のAWSインフラポートフォリオ、各リポジトリへの入り口となるトップページです。

Terraform + GitHub Actions でAWSインフラをコードで管理しています。
dev（開発）・staging（負荷試験・障害試験）・production（本番）の3環境を、nonprod（dev/staging）とprod（production）の2つのAWSアカウントに分離し、staging で検証した構成とイメージをそのまま production に適用しています。

## ディレクトリ構成

```
Tomario（ポートフォリオ全体）
├── tomario-infra/          … Terraformによるインフラ管理
│   ├── envs/                 … 環境別コード（nonprod/dev,staging,shared・prod/production）
│   ├── modules/              … network/backend/database/frontend/security/waf/monitoring/logging/cost/ecr/rds-autostop/secret-rotation
│   ├── lambda/               … RDSの自動停止・SECRET_KEYのローテーション用Lambda
│   ├── bootstrap-nonprod/    … nonprodアカウントのOIDC/IAM初期セットアップ
│   ├── bootstrap-prod/       … prodアカウントのOIDC/IAM初期セットアップ
│   ├── .github/workflows/    … plan/applyのCI/CD、cost-stop/start、セキュリティスタックの切り替え
│   └── docs/                 … アーキテクチャ構成図・運用手順
├── tomario-app/            … Flask API + 静的フロントエンド
│   ├── app.py                … API（認証・ホテル/客室検索・予約・キャンセル）
│   ├── frontend/             … 画面（HTML/CSS/JavaScript、S3+CloudFrontで配信）
│   └── .github/workflows/    … イメージのビルド・脆弱性スキャン・dev/stagingへのデプロイ・productionへの昇格
├── tomario-docs/           … 設計ドキュメント
│   ├── requirements/           … 要件定義書・非機能要件定義書
│   ├── basic-design/           … 基本設計書
│   ├── environment-definitions/ … 環境定義書
│   └── portfolio-constraints.md … 設計書と実際の運用の差分（ポートフォリオとしての運用上の制約）
└── tomario-steering/       … 設計判断の記録・試験・リリース管理
    ├── adr/                    … ADR（設計判断の背景・理由）
    ├── verification/           … 非機能試験の計画・手順・結果
    ├── operations/             … 障害対応手順（ランブック）
    └── release-management/     … リリース判定・カットオーバー・切り戻し
```

## リポジトリ

| リポジトリ | 内容 |
|---|---|
| [tomario-infra](https://github.com/Tomario-portfolio/tomario-infra) | Terraformによるインフラ管理（12モジュール構成、nonprod/prodアカウント分離） |
| [tomario-app](https://github.com/Tomario-portfolio/tomario-app) | Flask API + 静的フロントエンド |
| [tomario-docs](https://github.com/Tomario-portfolio/tomario-docs) | 要件定義書・基本設計書・環境定義書 |
| [tomario-steering](https://github.com/Tomario-portfolio/tomario-steering) | ADR・非機能試験・運用手順・リリース管理 |
