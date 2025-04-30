# floating-in-app-message
Brazeのアプリ内メッセージ（IAM）をフローティングのポップアップとしてWebページ内に表示したい場合のサンプルです。

## 利用前提
- こちらのサンプルでは、WebSDKをCDNで呼び出しを行っています。
- Brazeのダッシュボードにアクセスでき、Web SDK用のAPIキーおよびエンドポイントが取得できることが前提となります。

## サンプル稼働の確認手順
1. index.htmlおよび/imgディレクトリをダウンロードし、index.htmlを開きます。
2. index.htmlを編集し、braze.initializeのAPIキーおよびエンドポイントを変更します。
```
 // Braze SDKを初期化
 braze.initialize("YOUR-API-KEY-HERE", {
        baseUrl: "YOUR-SDK-ENDPOINT-HERE",
        allowUserSuppliedJavascript: true,  // HTMLベースのIAMの有効化
        minimumIntervalBetweenTriggerActionsInSeconds: 0, // 次のIAM表示までの間隔を0秒に設定
        enableLogging: true
});
```
3. Brazeの管理画面内でキャンペーンのページを開き、アプリ内メッセージのキャンペーンを作成します。
   - 送信先：Webブラウザー
   - メッセージタイプ：カスタムコード
   - メディアライブラリ：./img/quiz-campaign.png の画像を追加
   - HTML： ./iam-custom-code.html の内容を貼り付けてください。
        - 画像URLについては、上記のメディアライブラリにアップロードしたURLに置き換えてください。

4. メッセージ作成の「設定」タブで、index.html内で指定しているキーと値のペアを設定します。
   - キー：「floating」、値：「right.bottom」
   
5. 配信スケジュールで、index.html内で指定しているトリガーイベントを設定します。
   - カスタムイベントを実行： 「lp-iam-show」
   
6. ターゲットオーディエンスを設定し、index.htmlを開いたユーザーがターゲットに含まれるように設定します。
   - セグメントとして、All Users (xxx - Web) など
   
7. 設定確認まで進め、キャンペーンを保存します。

8.  キャンペーンが稼働している状態で、index.htmlをブラウザで開くと、設定したIAMがフローティングで表示されることが確認できるはずです。
