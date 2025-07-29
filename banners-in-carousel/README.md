# banners-in-carousel
Brazeの新機能BannersをWeb SDKにて取得し、カルーセル内に埋め込む場合のサンプルです。

## 利用前提
- Braze Web SDKの初期化が行われていること（サンプルコードのindex.html内のAPIキーおよびエンドポイントを置き換えてください）

## サンプルお試し手順（キャンペーンの作成方法）
1. Brazeの管理画面内でバナーのキャンペーンを作成します。
<img width="524" height="463" alt="image" src="https://github.com/user-attachments/assets/c8d2a54d-5525-4e79-8e84-a9987505efd8" />


2. メッセージ作成 > 配置(placement)の設定をします。
- 未設定の場合、「配置の管理」から新しい配置を作成できます。
- 配置を作成し、サンプルのコードに合わせて 配置ID（placement ID）をcarousel_banner1として設定してください。
<img width="1038" height="298" alt="image" src="https://github.com/user-attachments/assets/1dadc07c-3835-44da-8b98-7e4d7fb5984b" />


3. メッセージ作成 > 「バナーを作成」から表示されるバナーを編集します。
<img width="1331" height="768" alt="スクリーンショット 2025-07-29 15 18 51" src="https://github.com/user-attachments/assets/40d82fae-cef4-4beb-beba-26008103e143" />


4. ターゲットオーディエンスを設定します。
- ここではサイトを開いたユーザーが確実に対象になるように「All Users」などを選択してください。
- ABテストの設定も表示の確認のタイミングでは、コントロールグループを削除してください。
<img width="1070" height="680" alt="スクリーンショット 2025-07-29 15 19 49" src="https://github.com/user-attachments/assets/611f3cb2-821c-4dcc-9f03-ed86a7ebc0d4" />


5. キャンペーンを開始し、index.htmlを開きます。
