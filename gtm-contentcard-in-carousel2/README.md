# braze-gtm-contentcard-in-carousel2
Brazeのコンテンツカードのフルカスタマイズ実装例。
braze-gtm-contentcard-in-carouselのレートリミット対策版。
Web上のカルーセル内にカードの画像を埋め込む方法のサンプルです。

## レートリミット対策

Webサイトのトップページのみでコンテンツカードを利用する場合には、[braze-gtm-contentcard-in-carousel](https://github.com/jagainu/braze-examples/tree/main/gtm-contentcard-in-carousel)の実装で問題ない場合が多いのですが、`braze.requestContentCardsRefresh()` を各ページに埋め込むような場合で、短時間に複数ページを閲覧した場合には、レートリミットに引っかかり、コンテンツカードが読み込まれない問題が発生することがとざいます。

本実装では、braze-gtm-contentcard-in-carouselと同じ機能を維持したまま、以下のロジックでレートリミットを回避しています：

1. **初回訪問時**: `requestContentCardsRefresh()` を呼び出し、その日時をローカルストレージに記録
2. **3分以内の再訪問**: `getCachedContentCards()` からキャッシュされたカードを取得して表示
3. **3分以上経過後**: 再度 `requestContentCardsRefresh()` を呼び出してサーバーから最新を取得

### 設定可能なパラメータ

| 変数名 | デフォルト値 | 説明 |
|--------|-------------|------|
| `TARGET_ELEMENT_SELECTOR` | `'#img_contentcard-target'` | 上書きしたい要素のCSSセレクタ |
| `TARGET_FRAME_ID` | `'carousel_banner'` | Brazeで設定するキーと値のペアの値 |
| `REFRESH_INTERVAL_MS` | `3 * 60 * 1000` (3分) | リフレッシュ間隔（ミリ秒） |
| `LAST_REFRESH_KEY` | `'braze_contentcards_last_refresh'` | ローカルストレージのキー名 |

<!-- TODO: スクリーンショット - ローカルストレージに保存された値の確認画面 -->

## 利用前提
- Google Tag ManagerにてBraze Initialization Tagにて、Braze Web SDKの初期化が行われていること

## 利用手順
1. index.htmlおよび/imgディレクトリをダウンロードし、index.htmlを開きます。
   - カルーセルが表示されたページが確認できます。

![image](https://github.com/user-attachments/assets/0ba90b62-f08b-4e0b-933a-3ccfe3aafc7a)


2. index.htmlを編集しheaderにGTMのタグを入れます。

![image](https://github.com/user-attachments/assets/5882fa46-a9e7-41b4-8e33-46ea21101ac8)


3. GTMにてカスタムHTMLタグを作り、gtm-custom-html-tag.htmlの内容をコピーします。
   - 「document.write をサポートする」にチェック
   - Braze Initialization Tagの後にカスタムHTMLタグが発効するようにタグの順序を設定
   - 上記のindex.htmlが開かれた時にタグが発行するようにトリガーを設定

<!-- TODO: スクリーンショット - GTMカスタムHTMLタグの設定画面 -->


4. Brazeの管理画面内でコンテンツカードのキャンペーンを作成します。
   - セグメント
   - 画像のみで画像とリンク先のURLを入力します。

<!-- TODO: スクリーンショット - Brazeコンテンツカードキャンペーン作成画面 -->


5. コンテンツカードのキャンペーンの「設定」タブでキーと値のペアを設定します。
   - キー：「frame_id」、値：「carousel_banner」
   - このサンプルでは上記のキーと値のペアが設定されているコンテンツカードのうち、更新日が直近のものがカルーセルに埋め込まれるようになっています。

<!-- TODO: スクリーンショット - キーと値のペア設定画面 -->


6. ターゲットオーディエンスを設定し、キャンペーンを開始し、index.htmlを開きます。
   - キャンペーンのターゲットに含まれれば、コンテンツカードが配信され、カルーセルの最初の画像ファイルが差し代わるはずです。

<!-- TODO: スクリーンショット - コンテンツカード配信後のカルーセル表示 -->

## デバッグ方法

ブラウザの開発者ツールのコンソールで以下のログを確認できます：

- `"carousel-contentcards tag called"` - タグが呼び出された
- `"Refreshing content cards from server..."` - サーバーから最新を取得中
- `"Using cached content cards..."` - キャッシュから取得中

ローカルストレージの値は開発者ツールの「Application」タブから確認できます。

<!-- TODO: スクリーンショット - 開発者ツールでのデバッグ画面 -->
