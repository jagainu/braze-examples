# gtm-floating-iam
GTMを使って、Brazeのアプリ内メッセージ（IAM）をフローティングのポップアップとしてWebページ内に表示したい場合のサンプルです。
Braze公式のサンプルコードを参考にしています。
https://github.com/braze-inc/in-app-message-templates/tree/master/braze-templates/6-braze-nps

## 利用前提
- こちらのサンプルでは、WebSDKをGTMで呼び出しを行っています。
- Brazeのダッシュボードにアクセスでき、Web SDK用のAPIキーおよびエンドポイントが取得できることが前提となります。

## 実装のポイント
このサンプルのようにIAMをフローティング表示させるカスタマイズを行う上でのポイントとなる点は以下の通りです。
1. GTM Braze初期化タグのパラメーターとして以下を設定。
- Allow HTML In-App Messagesを有効化
- Automatically show new in app messagesを無効化
- Minimum Interval Between Triggered Messages: 0
（※デフォルトは30秒間たたないと次のIAMが表示できない。これを0秒に設定することによりすぐに次のIAMも表示できる）

2. カスタムHTMLにて初期化タグ直後に[braze.subscribeToInAppMessage()](https://js.appboycdn.com/web-sdk/latest/doc/modules/braze.html#subscribetoinappmessage)によりIAMを取得し、Key-valueペアの条件に合致するIAMの場合には追加のカスタマイズの処理を行い、表示する形で実装します。

3. Key-valueペアの条件に合致するIAMをキャンペーンにて設定します。

## サンプル稼働の確認手順
1. index.htmlおよび/imgディレクトリをダウンロードし、index.htmlを開きます。

2. index.htmlを編集しheaderにGTMのタグを入れます。

3. GTMにてBraze初期化タグをSDK APIキーやSDKエンドポイントを入れ、以下の設定を追加で行います。また、このindex.htmlが開かれた時にタグが発効するようにトリガーを設定します。
- Allow HTML In-App Messagesを有効化
- Automatically show new in app messagesを無効化
- Minimum Interval Between Triggered Messages: 0
<img width="2344" height="1480" alt="image" src="https://github.com/user-attachments/assets/a63fcbf3-7e79-4b87-8928-65effce0aae3" />

4. 新しくカスタムHTMLタグを作り（「subscribeToInAppMessage」タグ）、gtm-custom-html-tag.htmlの内容をコピーします。
   - 「document.write をサポートする」にチェック
   - このindex.htmlが開かれた時にタグが発効するようにトリガーを設定
   - Braze Initialization Tagの直後にこのカスタムHTMLタグが発効するようにタグの順序を設定
<img width="1475" height="734" alt="Screenshot 2025-12-12 at 17 34 46" src="https://github.com/user-attachments/assets/948ff213-0887-471b-8934-bc3bd17df539" />

3.次に、Braze Actionsタグを設定します。
   - このindex.htmlが開かれた時に、必要なタイミングでタグが発効するようにトリガーを設定（例：50%スクロールされた際に発火するイベント名「page_scroll_50%」）
   - 上記の、「subscribeToInAppMessage」タグの後にこのカスタムHTMLタグが発効するようにタグの順序を設定
<img width="1208" height="719" alt="Screenshot 2025-12-12 at 17 40 43" src="https://github.com/user-attachments/assets/6a3d4558-efd8-4505-9ec8-c145a9d03a6c" />


4. Brazeの管理画面内でキャンペーンのページを開き、アプリ内メッセージのキャンペーンを作成します。
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

6. また、テストのタイミングでは「ユーザーがキャンペーンを再度受信できるようにする」にチェックし、時間も「0分間」と設定すると、ページを読み込むたびにIAMが表示ができます。（本番ではメッセージ内容に合わせて設定を変えてください）
<img width="2648" height="1394" alt="image" src="https://github.com/user-attachments/assets/0b1dac2c-0159-401a-a9d9-5ac22acae236" />

7. ターゲットオーディエンスを設定し、index.htmlを開いたユーザーがターゲットに含まれるように設定します。
   - セグメントとして、All Users (xxx - Web) など
  
![image](https://github.com/user-attachments/assets/9ee14d15-421b-4dd1-987b-1c415583b3bf)
   
8. 設定確認まで進め、キャンペーンを保存します。

9. キャンペーンが稼働している状態で、index.htmlをブラウザで開くと、設定したIAMがフローティングで表示されることが確認できます。

うまく表示されない場合には、上記2〜6の設定を行ったキャンペーンが稼働しているか？Webブラウザのコンソールログを確認し、Web SDKの初期化がうまくいっているか？　IAMのトリガーとなるイベントが発火しているか？などをご確認ください。

![image](https://github.com/user-attachments/assets/1c1a1cf8-5b14-420d-9017-22b8b1a53eb8)

