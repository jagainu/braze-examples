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

## 利用手順 (gtm-contentcard-in-carouselと同様です)
1. index.htmlおよび/imgディレクトリをダウンロードし、index.htmlを開きます。
   - カルーセルが表示されたページが確認できます。

![image](https://github.com/user-attachments/assets/0ba90b62-f08b-4e0b-933a-3ccfe3aafc7a)


2. index.htmlを編集しheaderにGTMのタグを入れます。

![image](https://github.com/user-attachments/assets/5882fa46-a9e7-41b4-8e33-46ea21101ac8)


3. GTMにてカスタムHTMLタグを作り、gtm-custom-html-tag.htmlの内容をコピーします。
   - 「document.write をサポートする」にチェック
   - Braze Initialization Tagの後にカスタムHTMLタグが発効するようにタグの順序を設定
   - 上記のindex.htmlが開かれた時にタグが発行するようにトリガーを設定

<img width="1670" height="1018" alt="image" src="https://github.com/user-attachments/assets/b2e7d0f6-05f9-4403-aa68-cdd1e1a3689e" />



4. Brazeの管理画面内でコンテンツカードのキャンペーンを作成します。
   - セグメント
   - 画像のみで画像とリンク先のURLを入力します。

<img width="1696" height="1102" alt="image" src="https://github.com/user-attachments/assets/8be12b8a-14c9-454b-ac0d-bcd0437931f5" />



5. コンテンツカードのキャンペーンの「設定」タブでキーと値のペアを設定します。
   - キー：「frame_id」、値：「carousel_banner」
   - このサンプルでは上記のキーと値のペアが設定されているコンテンツカードのうち、更新日が直近のものがカルーセルに埋め込まれるようになっています。

<img width="1696" height="1102" alt="image" src="https://github.com/user-attachments/assets/0ac5991a-f092-4327-be2f-00eb0a73a13a" />



6. ターゲットオーディエンスを設定し、キャンペーンを開始し、index.htmlを開きます。
   - キャンペーンのターゲットに含まれれば、コンテンツカードが配信され、カルーセルの最初の画像ファイルが差し代わるはずです。

<img width="2238" height="874" alt="image" src="https://github.com/user-attachments/assets/0f1e1c65-054b-4873-9d74-01fe0ec126a4" />


## デバッグ方法

ブラウザの開発者ツールのコンソールで以下のログを確認できます：

- `"carousel-contentcards tag called"` - タグが呼び出された
- `"Refreshing content cards from server..."` - サーバーから最新を取得中
- `"Using cached content cards..."` - キャッシュから取得中

ローカルストレージの値は開発者ツールの「Application」タブから確認できます。
- Local Storage → braze_contentcards_last_refresh

<!-- TODO: スクリーンショット - 開発者ツールでのデバッグ画面 -->
