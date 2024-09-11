# braze-gtm-contentcard-in-carousel
BrazeのコンテンツカードをWeb上のカルーセル内に埋め込む場合のサンプルです。

## 利用前提
- Google Tag ManagerにてBraze Initialization Tagにて、Braze Web SDKの初期化が行われていること

## 利用手順
1. index.htmlおよび/imgディレクトリをダウンロードし、index.htmlを開きます。
   - カルーセルが表示されたページが確認できます。

![image](https://github.com/user-attachments/assets/46616a4d-85f3-41df-b702-5a960a0fb94c)

2. index.htmlを編集しheaderにGTMのタグを入れます。

<img width="720" alt="gtm1" src="https://github.com/user-attachments/assets/003317c7-1a4e-4336-9805-7605de320ee3">

3. GTMにてカスタムHTMLタグを作り、gtm-custom-html-tag.htmlの内容をコピーします。
   - 「document.write をサポートする」にチェック
   - Braze Initialization Tagの後にカスタムHTMLタグが発効するようにタグの順序を設定
   - 上記のindex.htmlが開かれた時にタグが発行するようにトリガーを設定

<img width="1079" alt="image" src="https://github.com/user-attachments/assets/fc7d1f2c-8ddf-4aaa-a340-22876196f073">

4. Brazeの管理画面内でコンテンツカードのキャンペーンを作成します。
   - セグメント
   - 画像のみで画像とリンク先のURLを入力します。

<img width="1081" alt="image" src="https://github.com/user-attachments/assets/b138010a-dc7c-4533-9f75-80241a8ce9a2">

5. コンテンツカードのキャンペーンの「設定」タブでキーと値のペアを設定します。
   - キー：「frame_id」、値：「carousel_banner」
   - このサンプルでは上記のキーと値のペアが設定されているコンテンツカードのうち、更新日が直近のものがカルーセルに埋め込まれるようになっています。

![image](https://github.com/user-attachments/assets/a218562b-6846-41d0-9e03-fbc4dd673565)

6. ターゲットオーディエンスを設定し、キャンペーンを開始し、index.htmlを開きます。
   - あなたがキャンペーンのターゲットに含まれれば、コンテンツカードが配信され、カルーセルの最初の画像ファイルが差し代わるはずです。

<img width="1133" alt="image" src="https://github.com/user-attachments/assets/e7908cbf-945e-4d22-9636-fd2c80bcf41f">

