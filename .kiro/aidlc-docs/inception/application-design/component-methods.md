# コンポーネントメソッド定義 - どんMai

## メソッドシグネチャ概要

各コンポーネントのメソッドシグネチャを定義します。詳細なビジネスロジックは Functional Design で定義されます。

---

## フロントエンド層メソッド

### ランディングページコンポーネント

```python
def render_landing_page() -> HTML
    """ランディングページをレンダリング"""
    # 入力: なし
    # 出力: HTML（ランディングページ）
    # 目的: サービス説明とデモへの導線を提供

def on_demo_button_click() -> None
    """デモボタンクリック時の処理"""
    # 入力: なし
    # 出力: なし
    # 目的: デモ体験画面に遷移
```

---

### デモ体験コンポーネント

```python
def render_demo_screen() -> HTML
    """デモ体験画面をレンダリング"""
    # 入力: なし
    # 出力: HTML（デモ体験画面）
    # 目的: デモ体験画面を表示

def on_generate_excuse_click(situation: str) -> str
    """言い訳生成ボタンクリック時の処理"""
    # 入力: situation（ユーザーの状況テキスト）
    # 出力: excuse（生成された言い訳）
    # 目的: 言い訳を生成して表示

def on_create_account_click() -> None
    """アカウント作成ボタンクリック時の処理"""
    # 入力: なし
    # 出力: なし
    # 目的: アカウント登録画面に遷移
```

---

### オンボーディングコンポーネント

```python
def render_onboarding_step(step: int) -> HTML
    """オンボーディングステップをレンダリング"""
    # 入力: step（ステップ番号 1-5）
    # 出力: HTML（オンボーディング画面）
    # 目的: 指定されたステップを表示

def on_plan_selected(plan: str) -> None
    """プラン選択時の処理"""
    # 入力: plan（"free" または "pro"）
    # 出力: なし
    # 目的: プラン選択を保存して次のステップに進む

def on_scene_selected(scenes: List[str]) -> None
    """シーン選択時の処理"""
    # 入力: scenes（選択されたシーンのリスト）
    # 出力: なし
    # 目的: シーン選択を保存してキャラクター表示に進む

def complete_onboarding() -> None
    """オンボーディング完了"""
    # 入力: なし
    # 出力: なし
    # 目的: オンボーディングを完了してホーム画面に遷移
```

---

### 言い訳生成UIコンポーネント

```python
def render_excuse_generation_screen() -> HTML
    """言い訳生成画面をレンダリング"""
    # 入力: なし
    # 出力: HTML（言い訳生成画面）
    # 目的: 言い訳生成画面を表示

def on_generate_excuse_click(situation: str) -> str
    """言い訳生成ボタンクリック時の処理"""
    # 入力: situation（ユーザーの状況テキスト）
    # 出力: excuse（生成された言い訳）
    # 目的: 言い訳を生成して表示

def display_excuse_history() -> List[str]
    """言い訳履歴を表示"""
    # 入力: なし
    # 出力: excuses（言い訳のリスト）
    # 目的: 過去の言い訳を表示

def on_pro_upgrade_click() -> None
    """Pro アップグレードボタンクリック時の処理"""
    # 入力: なし
    # 出力: なし
    # 目的: Pro 誘導モーダルを表示
```

---

### 懺悔室UIコンポーネント

```python
def render_confession_room_screen() -> HTML
    """懺悔室画面をレンダリング"""
    # 入力: なし
    # 出力: HTML（懺悔室画面）
    # 目的: 懺悔室画面を表示

def on_send_confession(confession: str) -> str
    """懺悔送信時の処理"""
    # 入力: confession（ユーザーの懺悔テキスト）
    # 出力: affirmation（肯定メッセージ）
    # 目的: 肯定メッセージを生成して表示

def display_confession_history() -> List[str]
    """懺悔履歴を表示"""
    # 入力: なし
    # 出力: confessions（懺悔のリスト）
    # 目的: 過去の懺悔を表示
```

---

### サボり肯定ポップアップコンポーネント

```python
def start_inactivity_monitoring() -> None
    """無操作監視を開始"""
    # 入力: なし
    # 出力: なし
    # 目的: mousemove/keydown イベント監視を開始

def on_user_activity() -> None
    """ユーザー操作時の処理"""
    # 入力: なし
    # 出力: なし
    # 目的: 無操作タイマーをリセット

def show_inactivity_popup() -> None
    """無操作ポップアップを表示"""
    # 入力: なし
    # 出力: なし
    # 目的: 30 秒無操作後にポップアップを表示

def close_popup() -> None
    """ポップアップを閉じる"""
    # 入力: なし
    # 出力: なし
    # 目的: ポップアップを閉じて監視を再開
```

---

### キャラクター表示コンポーネント

```python
def render_character(character_type: str) -> HTML
    """キャラクターをレンダリング"""
    # 入力: character_type（"default", "business", "casual", "fancy"）
    # 出力: HTML（キャラクター表示）
    # 目的: 指定されたキャラクターを表示

def animate_character() -> None
    """キャラクターアニメーション"""
    # 入力: なし
    # 出力: なし
    # 目的: キャラクターアニメーションを実行

def select_character_by_scene(scenes: List[str]) -> str
    """シーンに基づいてキャラクターを選択"""
    # 入力: scenes（選択されたシーンのリスト）
    # 出力: character_type（選択されたキャラクタータイプ）
    # 目的: シーンに基づいてキャラクターを決定
```

---

### 認証UIコンポーネント

```python
def render_login_screen() -> HTML
    """ログイン画面をレンダリング"""
    # 入力: なし
    # 出力: HTML（ログイン画面）
    # 目的: ログイン画面を表示

def on_login_submit(email: str, password: str) -> bool
    """ログイン送信時の処理"""
    # 入力: email（メールアドレス）, password（パスワード）
    # 出力: success（ログイン成功フラグ）
    # 目的: ログイン処理を実行

def on_google_login_click() -> None
    """Google ログインボタンクリック時の処理"""
    # 入力: なし
    # 出力: なし
    # 目的: Google ログイン画面に遷移

def render_signup_screen() -> HTML
    """登録画面をレンダリング"""
    # 入力: なし
    # 出力: HTML（登録画面）
    # 目的: 登録画面を表示

def on_signup_submit(email: str, password: str) -> bool
    """登録送信時の処理"""
    # 入力: email（メールアドレス）, password（パスワード）
    # 出力: success（登録成功フラグ）
    # 目的: 登録処理を実行
```

---

### 設定UIコンポーネント

```python
def render_settings_screen() -> HTML
    """設定画面をレンダリング"""
    # 入力: なし
    # 出力: HTML（設定画面）
    # 目的: 設定画面を表示

def display_plan_info() -> Dict
    """プラン情報を表示"""
    # 入力: なし
    # 出力: plan_info（プラン情報）
    # 目的: 現在のプラン情報を表示

def display_token_usage() -> Dict
    """トークン使用量を表示"""
    # 入力: なし
    # 出力: token_info（トークン使用情報）
    # 目的: トークン使用量を表示

def on_reset_character_click() -> None
    """キャラクターリセットボタンクリック時の処理"""
    # 入力: なし
    # 出力: なし
    # 目的: シーン選択画面に遷移

def on_logout_click() -> None
    """ログアウトボタンクリック時の処理"""
    # 入力: なし
    # 出力: なし
    # 目的: ログアウト処理を実行
```

---

## バックエンド層メソッド

### 認証サービス

```python
def authenticate_user(email: str, password: str) -> str
    """ユーザーを認証"""
    # 入力: email（メールアドレス）, password（パスワード）
    # 出力: token（JWT トークン）
    # 目的: ユーザーを認証して JWT トークンを発行

def verify_token(token: str) -> bool
    """JWT トークンを検証"""
    # 入力: token（JWT トークン）
    # 出力: valid（検証結果）
    # 目的: JWT トークンの有効性を検証

def register_user(email: str, password: str) -> str
    """ユーザーを登録"""
    # 入力: email（メールアドレス）, password（パスワード）
    # 出力: user_id（ユーザー ID）
    # 目的: 新規ユーザーを登録

def authenticate_with_google(google_token: str) -> str
    """Google トークンで認証"""
    # 入力: google_token（Google トークン）
    # 出力: token（JWT トークン）
    # 目的: Google トークンで認証して JWT トークンを発行
```

---

### 言い訳生成サービス

```python
def generate_excuse(situation: str, plan: str) -> str
    """言い訳を生成"""
    # 入力: situation（ユーザーの状況テキスト）, plan（"free" または "pro"）
    # 出力: excuse（生成された言い訳）
    # 目的: 言い訳を生成

def calculate_token_usage(excuse: str) -> int
    """トークン使用量を計算"""
    # 入力: excuse（生成された言い訳）
    # 出力: tokens（使用トークン数）
    # 目的: 言い訳生成に使用されたトークン数を計算
```

---

### 懺悔室サービス

```python
def generate_affirmation(confession: str) -> str
    """肯定メッセージを生成"""
    # 入力: confession（ユーザーの懺悔テキスト）
    # 出力: affirmation（肯定メッセージ）
    # 目的: 肯定メッセージを生成
```

---

### トークン管理サービス

```python
def record_token_usage(user_id: str, tokens: int) -> None
    """トークン使用量を記録"""
    # 入力: user_id（ユーザー ID）, tokens（使用トークン数）
    # 出力: なし
    # 目的: トークン使用量を記録

def get_remaining_tokens(user_id: str) -> int
    """残りトークン数を取得"""
    # 入力: user_id（ユーザー ID）
    # 出力: remaining_tokens（残りトークン数）
    # 目的: 残りトークン数を取得

def check_token_limit(user_id: str) -> bool
    """トークン上限をチェック"""
    # 入力: user_id（ユーザー ID）
    # 出力: within_limit（上限内フラグ）
    # 目的: トークン上限内かどうかをチェック

def reset_daily_tokens() -> None
    """1 日ごとのトークンをリセット"""
    # 入力: なし
    # 出力: なし
    # 目的: 毎日 0:00 JST にトークンをリセット
```

---

### プラン管理サービス

```python
def get_user_plan(user_id: str) -> str
    """ユーザーのプランを取得"""
    # 入力: user_id（ユーザー ID）
    # 出力: plan（"free" または "pro"）
    # 目的: ユーザーのプランを取得

def upgrade_to_pro(user_id: str) -> bool
    """Pro プランにアップグレード"""
    # 入力: user_id（ユーザー ID）
    # 出力: success（アップグレード成功フラグ）
    # 目的: ユーザーを Pro プランにアップグレード

def process_payment(user_id: str, amount: int) -> bool
    """支払いを処理"""
    # 入力: user_id（ユーザー ID）, amount（支払い金額）
    # 出力: success（支払い成功フラグ）
    # 目的: AWS Marketplace で支払いを処理
```

---

### キャラクター管理サービス

```python
def get_character_by_scenes(scenes: List[str]) -> str
    """シーンに基づいてキャラクターを取得"""
    # 入力: scenes（選択されたシーンのリスト）
    # 出力: character_type（キャラクタータイプ）
    # 目的: シーンに基づいてキャラクターを決定

def save_user_scenes(user_id: str, scenes: List[str]) -> None
    """ユーザーのシーン選択を保存"""
    # 入力: user_id（ユーザー ID）, scenes（選択されたシーンのリスト）
    # 出力: なし
    # 目的: ユーザーのシーン選択を保存

def reset_user_character(user_id: str) -> None
    """ユーザーのキャラクターをリセット"""
    # 入力: user_id（ユーザー ID）
    # 出力: なし
    # 目的: ユーザーのキャラクター設定をリセット
```

---

### 攻撃検知サービス

```python
def detect_prompt_injection(text: str) -> bool
    """プロンプトインジェクションを検知"""
    # 入力: text（ユーザーの入力テキスト）
    # 出力: is_injection（プロンプトインジェクション判定）
    # 目的: プロンプトインジェクションを検知

def detect_character_attack(text: str) -> bool
    """キャラクター攻撃を検知"""
    # 入力: text（ユーザーの入力テキスト）
    # 出力: is_attack（キャラクター攻撃判定）
    # 目的: キャラクター攻撃を検知

def generate_defense_message() -> str
    """防御メッセージを生成"""
    # 入力: なし
    # 出力: message（防御メッセージ）
    # 目的: 攻撃に対する防御メッセージを生成
```

---

### 言い訳履歴サービス

```python
def save_excuse(user_id: str, excuse: str, scene: str) -> None
    """言い訳を保存"""
    # 入力: user_id（ユーザー ID）, excuse（言い訳テキスト）, scene（シーン）
    # 出力: なし
    # 目的: 言い訳を保存

def get_excuse_history(user_id: str) -> List[str]
    """言い訳履歴を取得"""
    # 入力: user_id（ユーザー ID）
    # 出力: excuses（言い訳のリスト）
    # 目的: ユーザーの言い訳履歴を取得

def delete_excuse(user_id: str, excuse_id: str) -> None
    """言い訳を削除"""
    # 入力: user_id（ユーザー ID）, excuse_id（言い訳 ID）
    # 出力: なし
    # 目的: 言い訳を削除
```

---

### API ゲートウェイ

```python
def route_request(method: str, path: str, body: Dict) -> Dict
    """リクエストをルーティング"""
    # 入力: method（HTTP メソッド）, path（パス）, body（リクエストボディ）
    # 出力: response（レスポンス）
    # 目的: リクエストを適切なサービスにルーティング

def validate_authentication(token: str) -> bool
    """認証を検証"""
    # 入力: token（JWT トークン）
    # 出力: valid（検証結果）
    # 目的: リクエストの認証を検証

def format_response(data: Dict, status: int) -> Dict
    """レスポンスを形式化"""
    # 入力: data（レスポンスデータ）, status（ステータスコード）
    # 出力: response（形式化されたレスポンス）
    # 目的: レスポンスを標準形式で返す
```

---

### エラーハンドラー

```python
def handle_error(error: Exception) -> Dict
    """エラーを処理"""
    # 入力: error（エラーオブジェクト）
    # 出力: error_response（エラーレスポンス）
    # 目的: エラーをキャッチして適切なレスポンスを生成

def log_error(error: Exception) -> None
    """エラーをログに記録"""
    # 入力: error（エラーオブジェクト）
    # 出力: なし
    # 目的: エラーを CloudWatch にログ

def classify_error(error: Exception) -> str
    """エラーを分類"""
    # 入力: error（エラーオブジェクト）
    # 出力: error_type（エラータイプ）
    # 目的: エラーを分類して適切に処理
```

---

## データ層メソッド

### ユーザーテーブル

```python
def create_user(email: str, password_hash: str) -> str
    """ユーザーを作成"""
    # 入力: email（メールアドレス）, password_hash（パスワードハッシュ）
    # 出力: user_id（ユーザー ID）

def get_user(user_id: str) -> Dict
    """ユーザーを取得"""
    # 入力: user_id（ユーザー ID）
    # 出力: user（ユーザー情報）

def update_user_plan(user_id: str, plan: str) -> None
    """ユーザーのプランを更新"""
    # 入力: user_id（ユーザー ID）, plan（プラン）
    # 出力: なし

def update_user_scenes(user_id: str, scenes: List[str]) -> None
    """ユーザーのシーン選択を更新"""
    # 入力: user_id（ユーザー ID）, scenes（シーンのリスト）
    # 出力: なし
```

---

### トークン使用量テーブル

```python
def record_token_usage(user_id: str, date: str, tokens: int) -> None
    """トークン使用量を記録"""
    # 入力: user_id（ユーザー ID）, date（日付）, tokens（使用トークン数）
    # 出力: なし

def get_token_usage(user_id: str, date: str) -> int
    """トークン使用量を取得"""
    # 入力: user_id（ユーザー ID）, date（日付）
    # 出力: tokens（使用トークン数）

def reset_daily_tokens(date: str) -> None
    """1 日ごとのトークンをリセット"""
    # 入力: date（日付）
    # 出力: なし
```

---

### 言い訳履歴テーブル

```python
def save_excuse(user_id: str, excuse: str, scene: str, timestamp: str) -> str
    """言い訳を保存"""
    # 入力: user_id（ユーザー ID）, excuse（言い訳テキスト）, scene（シーン）, timestamp（タイムスタンプ）
    # 出力: excuse_id（言い訳 ID）

def get_excuse_history(user_id: str) -> List[Dict]
    """言い訳履歴を取得"""
    # 入力: user_id（ユーザー ID）
    # 出力: excuses（言い訳のリスト）

def delete_excuse(excuse_id: str) -> None
    """言い訳を削除"""
    # 入力: excuse_id（言い訳 ID）
    # 出力: なし
```

