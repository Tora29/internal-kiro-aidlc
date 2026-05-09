# サービス層設計 - どんMai

## サービス層概要

「どんMai」のバックエンド層は、マイクロサービスアーキテクチャで設計されています。各サービスは独立した責務を持ち、API ゲートウェイを通じて通信します。

---

## サービス定義

### 1. 認証サービス (Authentication Service)

**責務**: ユーザー認証と認可を管理

**主要機能**:
- Cognito との連携
- JWT トークンの発行と検証
- ユーザーセッション管理
- Google ソーシャルログイン対応

**API エンドポイント**:
- `POST /auth/login` - ユーザーログイン
- `POST /auth/signup` - ユーザー登録
- `POST /auth/google-login` - Google ログイン
- `POST /auth/verify-token` - トークン検証
- `POST /auth/logout` - ログアウト

**依存関係**: Amazon Cognito

**通信パターン**: REST API

---

### 2. 言い訳生成サービス (Excuse Generation Service)

**責務**: ユーザーの状況に応じた言い訳を生成

**主要機能**:
- Amazon Bedrock との連携
- Claude Haiku/Sonnet の選択
- プロンプトエンジニアリング
- トークン使用量の計算
- 言い訳履歴への保存

**API エンドポイント**:
- `POST /excuses/generate` - 言い訳を生成
- `GET /excuses/history` - 言い訳履歴を取得
- `DELETE /excuses/{excuse_id}` - 言い訳を削除

**依存関係**: Amazon Bedrock、言い訳履歴サービス、トークン管理サービス

**通信パターン**: REST API

---

### 3. 懺悔室サービス (Confession Room Service)

**責務**: ユーザーの懺悔に対して肯定メッセージを生成

**主要機能**:
- Amazon Bedrock との連携
- Claude Haiku による肯定メッセージ生成
- プロンプトエンジニアリング

**API エンドポイント**:
- `POST /confessions/send` - 懺悔を送信
- `GET /confessions/history` - 懺悔履歴を取得

**依存関係**: Amazon Bedrock

**通信パターン**: REST API

---

### 4. トークン管理サービス (Token Management Service)

**責務**: ユーザーのトークン使用量を管理

**主要機能**:
- トークン使用量の記録
- 1 日ごとのリセット
- トークン上限チェック
- Free/Pro プランの区別

**API エンドポイント**:
- `POST /tokens/record` - トークン使用量を記録
- `GET /tokens/remaining` - 残りトークン数を取得
- `GET /tokens/check-limit` - トークン上限をチェック

**依存関係**: DynamoDB、プラン管理サービス

**通信パターン**: REST API

---

### 5. プラン管理サービス (Plan Management Service)

**責務**: ユーザーのプラン情報を管理

**主要機能**:
- Free/Pro プランの管理
- プラン切り替え
- AWS Marketplace との連携
- サブスクリプション管理

**API エンドポイント**:
- `GET /plans/user-plan` - ユーザーのプランを取得
- `POST /plans/upgrade-to-pro` - Pro プランにアップグレード
- `POST /plans/process-payment` - 支払いを処理

**依存関係**: DynamoDB、AWS Marketplace

**通信パターン**: REST API

---

### 6. キャラクター管理サービス (Character Management Service)

**責務**: キャラクター分岐ロジックを管理

**主要機能**:
- シーン選択に基づくキャラクター分岐
- キャラクター情報の取得
- キャラクターリセット

**API エンドポイント**:
- `POST /characters/select` - キャラクターを選択
- `GET /characters/info` - キャラクター情報を取得
- `POST /characters/reset` - キャラクターをリセット

**依存関係**: DynamoDB

**通信パターン**: REST API

---

### 7. 攻撃検知サービス (Attack Detection Service)

**責務**: プロンプトインジェクションとキャラクター攻撃を検知

**主要機能**:
- プロンプトインジェクション検知
- キーワードベースの攻撃検知
- 攻撃時の対応メッセージ生成

**API エンドポイント**:
- `POST /security/detect-attack` - 攻撃を検知
- `GET /security/defense-message` - 防御メッセージを取得

**依存関係**: なし

**通信パターン**: REST API

---

### 8. 言い訳履歴サービス (Excuse History Service)

**責務**: ユーザーの言い訳履歴を管理

**主要機能**:
- 言い訳の保存
- 言い訳の取得
- 言い訳の削除

**API エンドポイント**:
- `POST /excuse-history/save` - 言い訳を保存
- `GET /excuse-history/list` - 言い訳履歴を取得
- `DELETE /excuse-history/{excuse_id}` - 言い訳を削除

**依存関係**: DynamoDB

**通信パターン**: REST API

---

## サービス間通信パターン

### 言い訳生成フロー

```
フロントエンド
  ↓
API ゲートウェイ
  ↓
言い訳生成サービス
  ├→ Amazon Bedrock（言い訳生成）
  ├→ トークン管理サービス（トークン使用量を記録）
  └→ 言い訳履歴サービス（言い訳を保存）
  ↓
フロントエンド
```

### Pro アップグレードフロー

```
フロントエンド
  ↓
API ゲートウェイ
  ↓
プラン管理サービス
  ├→ AWS Marketplace（支払い処理）
  └→ DynamoDB（プラン情報を更新）
  ↓
フロントエンド
```

### 攻撃検知フロー

```
フロントエンド
  ↓
API ゲートウェイ
  ↓
攻撃検知サービス
  ├→ プロンプトインジェクション検知
  └→ キャラクター攻撃検知
  ↓
フロントエンド（防御メッセージを表示）
```

---

## オーケストレーションパターン

### 同期オーケストレーション

**言い訳生成**:
1. フロントエンドが言い訳生成リクエストを送信
2. API ゲートウェイが認証を検証
3. 言い訳生成サービスが言い訳を生成
4. トークン管理サービスがトークン使用量を記録
5. 言い訳履歴サービスが言い訳を保存
6. フロントエンドが言い訳を表示

### 非同期オーケストレーション

**ログ記録**:
1. サービスがイベントを生成
2. CloudWatch にログを記録（非同期）
3. メトリクスを記録（非同期）

**支払い処理**:
1. プラン管理サービスが支払いリクエストを送信
2. AWS Marketplace が支払いを処理（非同期）
3. 支払い完了後にプラン情報を更新

---

## サービス依存関係マトリックス

| サービス | 認証 | 言い訳生成 | 懺悔室 | トークン | プラン | キャラクター | 攻撃検知 | 履歴 |
|--------|------|---------|------|--------|------|----------|--------|------|
| 認証 | - | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| 言い訳生成 | ✓ | - | | ✓ | ✓ | | | ✓ |
| 懺悔室 | ✓ | | - | | | | | |
| トークン | ✓ | ✓ | | - | ✓ | | | |
| プラン | ✓ | ✓ | | ✓ | - | | | |
| キャラクター | ✓ | | | | | - | | |
| 攻撃検知 | ✓ | ✓ | ✓ | | | | - | |
| 履歴 | ✓ | ✓ | | | | | | - |

---

## サービス間通信プロトコル

### REST API

**ベース URL**: `https://api.donmai.example.com`

**認証**: JWT トークン（Authorization ヘッダー）

**レスポンス形式**:
```json
{
  "status": "success",
  "data": { ... },
  "error": null
}
```

**エラーレスポンス形式**:
```json
{
  "status": "error",
  "data": null,
  "error": {
    "code": "ERROR_CODE",
    "message": "エラーメッセージ"
  }
}
```

---

## サービスデプロイメント

### AWS Lambda

各サービスは独立した AWS Lambda 関数として実装されます。

**デプロイメント構成**:
- 言い訳生成サービス: `lambda-excuse-generation`
- 懺悔室サービス: `lambda-confession-room`
- トークン管理サービス: `lambda-token-management`
- プラン管理サービス: `lambda-plan-management`
- キャラクター管理サービス: `lambda-character-management`
- 攻撃検知サービス: `lambda-attack-detection`
- 言い訳履歴サービス: `lambda-excuse-history`
- 認証サービス: `lambda-authentication`

### API ゲートウェイ

API ゲートウェイが全サービスのエンドポイントを統合します。

**ルーティング**:
- `/auth/*` → 認証サービス
- `/excuses/*` → 言い訳生成サービス
- `/confessions/*` → 懺悔室サービス
- `/tokens/*` → トークン管理サービス
- `/plans/*` → プラン管理サービス
- `/characters/*` → キャラクター管理サービス
- `/security/*` → 攻撃検知サービス
- `/excuse-history/*` → 言い訳履歴サービス

---

## スケーラビリティ考慮事項

### Lambda オートスケーリング

各サービスは Lambda のオートスケーリング機能を活用します。

- **同時実行数**: 1000（デフォルト）
- **タイムアウト**: 30 秒
- **メモリ**: 512 MB（サービスごとに調整可能）

### DynamoDB スケーリング

DynamoDB はオンデマンド課金モデルを使用します。

- **読み取り容量**: オンデマンド
- **書き込み容量**: オンデマンド
- **自動スケーリング**: 有効

### キャッシング戦略

ElastiCache を使用した分散キャッシングを実装します。

- **キャッシュ対象**: ユーザー情報、プラン情報、キャラクター情報
- **TTL**: 1 時間
- **キャッシュ無効化**: ユーザー情報更新時

