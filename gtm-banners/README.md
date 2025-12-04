# banners-in-carousel
Braze Web SDKにてBannersのデータを取得し、ページのトップにある<div>タグ内にバナーを埋め込む場合のサンプルです。

## 利用前提
- Google Tag ManagerにてBraze Initialization Tagにて、Braze Web SDKの初期化が行われていること

## 利用手順
1. index.htmlおよび/imgディレクトリをダウンロードし、index.htmlを開きます。
<img width="1341" height="937" alt="image" src="https://github.com/user-attachments/assets/67a497b4-75c1-4e57-b437-223b16a225ec" />
最初はBannersの読み込みがされていないため、ページトップにバナーは表示されていません。

2. index.htmlを編集しheaderにGTMのタグを入れます。


3. GTMにてカスタムHTMLタグを作り、gtm-custom-html-tag.htmlの内容をコピーします。
   - 「document.write をサポートする」にチェック
   - Braze Initialization Tagの後にカスタムHTMLタグが発効するようにタグの順序を設定
   - 上記のindex.htmlが開かれた時にタグが発行するようにトリガーを設定


4. Brazeの管理画面内でバナーのキャンペーンを作成します。



5. メッセージ作成 > 配置(placement)の設定をします。
- 未設定の場合、「配置の管理」から新しい配置を作成できます。
- 配置を作成し、サンプルのコードに合わせて 配置ID（placement ID）をheader_banner1として設定してください。

<img width="995" height="375" alt="image" src="https://github.com/user-attachments/assets/f56d3ee1-521c-43ab-b61b-6d499936f90a" />


6. メッセージ作成 > 「バナーを作成」から表示されるバナーを編集します。

<img width="1290" height="823" alt="image" src="https://github.com/user-attachments/assets/11a566b0-57ce-452d-8aed-78196caaf642" />


7. ターゲットオーディエンスを設定します。
- ここではサイトを開いたユーザーが確実に対象になるように「All Users」などを選択してください。

<img width="1021" height="442" alt="image" src="https://github.com/user-attachments/assets/891ccb93-322f-49e3-9c13-12b28cdfc123" />

- ABテストの設定も表示の確認のタイミングでは、コントロールグループを削除してください。
<img width="1018" height="582" alt="image" src="https://github.com/user-attachments/assets/cddfa4ff-1fb1-4ede-acdd-c0be49d2c8a9" />


8. キャンペーンを開始し、index.htmlを開きます。

<img width="1299" height="836" alt="image" src="https://github.com/user-attachments/assets/15b75f47-130d-4ee9-a9ff-3df91fd6ba06" />
ページトップにバナーが読み込みれたことが確認できます。
