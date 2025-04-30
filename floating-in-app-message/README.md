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

![image](https://github.com/user-attachments/assets/24574ce4-7a37-4bd0-9198-0648f1747f37)

4. メッセージ作成の「設定」タブで、index.html内で指定しているキーと値のペアを設定します。
   - キー：「floating」、値：「right.bottom」
  
![image](https://github.com/user-attachments/assets/aeb5fb7b-56a1-4545-b778-6ec54cd90203)
   
5. 配信スケジュールで、index.html内で指定しているトリガーイベントを設定します。
   - カスタムイベントを実行： 「lp-iam-show」

![image](https://github.com/user-attachments/assets/373e443b-0b4b-487c-ac17-e15762ba0938)

6. ターゲットオーディエンスを設定し、index.htmlを開いたユーザーがターゲットに含まれるように設定します。
   - セグメントとして、All Users (xxx - Web) など
  
![image](https://github.com/user-attachments/assets/9ee14d15-421b-4dd1-987b-1c415583b3bf)

   
8. 設定確認まで進め、キャンペーンを保存します。

9.  キャンペーンが稼働している状態で、index.htmlをブラウザで開くと、設定したIAMがフローティングで表示されることが確認できます。

うまく表示されない場合には、上記2〜6の設定を行ったキャンペーンが稼働しているか？Webブラウザのコンソールログを確認し、Web SDKの初期化がうまくいっているか？　IAMのトリガーとなるイベントが発火しているか？などをご確認ください。

![image](https://github.com/user-attachments/assets/1c1a1cf8-5b14-420d-9017-22b8b1a53eb8)

