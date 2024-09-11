# braze-gtm-contentcard-in-carousel
BrazeのコンテンツカードをWeb上のカルーセル内に埋め込む場合のサンプルです。

## 利用前提
- Google Tag ManagerにてBraze Initialization Tagにて、Braze Web SDKの初期化が行われていること

## 利用手順
1. index.htmlおよび/imgディレクトリをダウンロードし、index.htmlを開きます。
   - カルーセルが表示されたページが確認できます。
   - 
![image](https://github.com/user-attachments/assets/0ba90b62-f08b-4e0b-933a-3ccfe3aafc7a)


2. index.htmlを編集しheaderにGTMのタグを入れます。

![image](https://github.com/user-attachments/assets/5882fa46-a9e7-41b4-8e33-46ea21101ac8)


3. GTMにてカスタムHTMLタグを作り、gtm-custom-html-tag.htmlの内容をコピーします。
   - 「document.write をサポートする」にチェック
   - Braze Initialization Tagの後にカスタムHTMLタグが発効するようにタグの順序を設定
   - 上記のindex.htmlが開かれた時にタグが発行するようにトリガーを設定

<img width="932" alt="image" src="https://github.com/user-attachments/assets/9c8fd944-e653-4fdf-b745-c1568b323c9f">


4. Brazeの管理画面内でコンテンツカードのキャンペーンを作成します。
   - セグメント
   - 画像のみで画像とリンク先のURLを入力します。

<img width="835" alt="image" src="https://github.com/user-attachments/assets/d12ae95d-1dd6-4c2b-ad39-bf743d8572e5">


5. コンテンツカードのキャンペーンの「設定」タブでキーと値のペアを設定します。
   - キー：「frame_id」、値：「carousel_banner」
   - このサンプルでは上記のキーと値のペアが設定されているコンテンツカードのうち、更新日が直近のものがカルーセルに埋め込まれるようになっています。

![image](https://github.com/user-attachments/assets/5f524ae8-58b2-49a8-9917-76eb260bbf2e)


6. ターゲットオーディエンスを設定し、キャンペーンを開始し、index.htmlを開きます。
   - あなたがキャンペーンのターゲットに含まれれば、コンテンツカードが配信され、カルーセルの最初の画像ファイルが差し代わるはずです。

<img width="1119" alt="image" src="https://github.com/user-attachments/assets/24f043ca-f40e-4d4a-920a-37aa7918b7eb">


