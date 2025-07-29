# banners-in-carousel
Brazeの新機能BannersをWeb SDKにて取得し、カルーセル内に埋め込む場合のサンプルです。

## 利用前提
- Braze Web SDKの初期化が行われていること（サンプル内のAPIキーおよびエンドポイントを置き換えてください）

## 利用手順（キャンペーンの作成方法）
1. Brazeの管理画面内でバナーのキャンペーンを作成します。
   - セグメント
   - 画像のみで画像とリンク先のURLを入力します。

<img width="835" alt="image" src="https://github.com/user-attachments/assets/d12ae95d-1dd6-4c2b-ad39-bf743d8572e5">


2. コンテンツカードのキャンペーンの「設定」タブでキーと値のペアを設定します。
   - キー：「frame_id」、値：「carousel_banner」
   - このサンプルでは上記のキーと値のペアが設定されているコンテンツカードのうち、更新日が直近のものがカルーセルに埋め込まれるようになっています。

![image](https://github.com/user-attachments/assets/5f524ae8-58b2-49a8-9917-76eb260bbf2e)


3. ターゲットオーディエンスを設定し、キャンペーンを開始し、index.htmlを開きます。
   - あなたがキャンペーンのターゲットに含まれれば、コンテンツカードが配信され、カルーセルの最初の画像ファイルが差し代わるはずです。

<img width="1119" alt="image" src="https://github.com/user-attachments/assets/24f043ca-f40e-4d4a-920a-37aa7918b7eb">