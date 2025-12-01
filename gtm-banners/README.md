# banners-in-carousel
Brazeの新機能BannersをWeb SDKにて取得し、カルーセル内に埋め込む場合のサンプルです。

## 利用前提
- Google Tag ManagerにてBraze Initialization Tagにて、Braze Web SDKの初期化が行われていること

## 利用手順
1. index.htmlおよび/imgディレクトリをダウンロードし、index.htmlを開きます。
   - カルーセルが表示されたページが確認できます。


2. index.htmlを編集しheaderにGTMのタグを入れます。


3. GTMにてカスタムHTMLタグを作り、gtm-custom-html-tag.htmlの内容をコピーします。
   - 「document.write をサポートする」にチェック
   - Braze Initialization Tagの後にカスタムHTMLタグが発効するようにタグの順序を設定
   - 上記のindex.htmlが開かれた時にタグが発行するようにトリガーを設定


4. Brazeの管理画面内でバナーのキャンペーンを作成します。



5. メッセージ作成 > 配置(placement)の設定をします。
- 未設定の場合、「配置の管理」から新しい配置を作成できます。
- 配置を作成し、サンプルのコードに合わせて 配置ID（placement ID）をheader_banner1として設定してください。



6. メッセージ作成 > 「バナーを作成」から表示されるバナーを編集します。



7. ターゲットオーディエンスを設定します。
- ここではサイトを開いたユーザーが確実に対象になるように「All Users」などを選択してください。
- ABテストの設定も表示の確認のタイミングでは、コントロールグループを削除してください。


8. キャンペーンを開始し、index.htmlを開きます。
