# **ラボ 03: Teams のチーム、共同作業、アプリ設定を管理する**

# **受講者用ラボ解答**

## **ラボ シナリオ**

このコースのラボでは、Contoso Ltd. の Teams 管理者である Joni Sherman の役割を担います。このラボでは、既存のグループからのチーム作成など、Teams 管理者としての運用タスクを実施します[…]

Microsoft Teams におけるコラボレーションの管理では、チーム設定やプライベート チャネル作成ポリシーなど、チャットと共同作業のエクスペリエンスを管理します。最後に、Teams のアプリ設定も管理します[…]

## **目標**

このラボを完了すると、次のことができるようになります。

- Microsoft 365 グループからチームを作成する
- PowerShell を使用してチームを作成する
- Microsoft Graph API を使用してチームを作成する
- 動的メンバーシップのチームを作成する
- Teams をアーカイブ/アーカイブ解除する
- Teams を削除/復元する
- メッセージング ポリシーを作成する
- プライベート チャネルを管理する
- サードパーティ ストレージ プロバイダーを無効にする
- ポリシー パッケージを管理する
- 既定の組織全体のアプリ ポリシーを編集/テストする
- 既定のアプリのアクセス許可ポリシーを編集/テストする
- カスタムのアプリの設定ポリシーを作成/管理する

## **ラボ セットアップ**

- **推定時間:** 110 分

## **手順**

### **演習 1: チーム リソースを管理する**

#### タスク 1 - 既存の Microsoft 365 グループからチームを作成する

Contoso のパイロット プロジェクトの一環として、以前のラボで作成した Microsoft 365 グループ **IT-Department** を変更し、Teams の機能を追加する必要があります。

1. 提供された資格情報で **Client 1 VM** に接続します。

2. タスクバーの **Teams** アイコンを選択して Teams デスクトップ クライアントを起動し、**Joni Sherman**（JoniS@&lt;YourTenant&gt;.OnMicrosoft.com）としてサインインします。

3. Microsoft Teams デスクトップ クライアントが起動します。**チームをまとめましょう** や **Teams モバイル アプリを入手** のウィンドウが表示された場合は閉じます。

4. 左側のナビゲーションで **Teams** を選択し、**+** を選んで **チームを作成** を選択します。

5. **チームを作成** ダイアログで、**他の作成オプション** を選び、**グループから** を選択します。

6. **どの Microsoft 365 グループを使用しますか?** ダイアログで、��ループ **“IT-Department”** を選び、**チームを追加** を押します。**チームを作成しています…** が完了するまで待ちます。

8. 左ペインの新しいチームの右側にある三点リーダー（**…**）を選択し、**チームの管理** を選択します。

9. チームの所有者とメンバーを確認します:

   - 所有者: **Joni Sherman**
   - メンバーとゲスト: **Allan Deyoung**、**MOD Administrator**、**Patti Fernandez**

10. Teams デスクトップ クライアントは開いたまま、次のタスクに進みます。

既存の Microsoft 365 グループを使用し、Teams デスクトップ クライアントで新しいチームを作成できました。Teams クライアントは開いたまま次へ進んでください。

#### タスク 2 - PowerShell を使用してチームを作成する

このタスクでは、Teams PowerShell を使って新しいチーム **“CA-Office”** を作成します。パブリック チャネル **“Support”** と **“Recruiting”** を作成し、さらに[…]

1. 提供された資格情報で **Client 1 VM** に接続します。

2. 画面下部のタスクバーで **スタート** を右クリックし、**Windows PowerShell** を選択します。

3. 次のコマンドレットを実行して、テナント内の Microsoft Teams に接続します:

    ```powershell
    Connect-MicrosoftTeams
    ```

4. **サインイン** ダイアログが開きます。提供された **Joni Sherman** の **UPN**（例: JoniS@&lt;YourTenant&gt;.onmicrosoft.com）を入力し、**次へ** を選択します。

5. **パスワードの入力** ダイアログで、提供された **Joni Sherman** の **パスワード** を入力し、**サインイン** を選択します。

6. 新しいチーム **CA-Office** を作成するため、PowerShell ウィンドウで次のコマンドレットを入力します:

    ```powershell
    New-Team -Displayname "CA-Office" -MailNickName "CA-Office" -Visibility Public
    ```

7. ユーザー **Alex Wilber** をチームに追加します（<YourTenant> を提供された Microsoft 365 テナント名に置換）:

    ```powershell
    Get-Team -Displayname "CA-Office" | Add-TeamUser -User AlexW@<YourTenant>.OnMicrosoft.com
    ```

8. ユーザー **Allan Deyoung** をチームに追加します（<YourTenant> を置換）:

    ```powershell
    Get-Team -Displayname "CA-Office" | Add-TeamUser -User AllanD@<YourTenant>.onmicrosoft.com
    ```

9. **CA-Office** チームに **Support** チャネルを作成します:

    ```powershell
    Get-Team -Displayname "CA-Office" | New-TeamChannel -DisplayName "Support"
    ```

10. **CA-Office** チームに **Recruiting** チャネルを作成します:

    ```powershell
    Get-Team -Displayname "CA-Office" | New-TeamChannel -DisplayName "Recruiting"
    ```

11. **CA-Office** チームにプライベート チャネル **Administration** を作成します:

    ```powershell
    Get-Team -Displayname "CA-Office" | New-TeamChannel -DisplayName "Administration" -MembershipType Private
    ```

12. Microsoft Teams から切断します。  

    ```powershell
    Disconnect-MicrosoftTeams
    ```

13. PowerShell ウィンドウを閉じます。

14. タスクバーから Teams デスクトップ クライアントを開きます。左ペインのチーム一覧で、Joni は新しい **CA-Office** チームのメンバーになっており、下に「Administration」というプライベート チャネルが見えるはずです[…]

15. すべてのブラウザー ウィンドウと Teams デスクトップ クライアントを閉じます。

**CA-Office** というチームを、メンバー Alex Wilber と Allan Deyoung で作成できました。Joni Sherman が唯一のチーム所有者です。PowerShell では所有者を指定していない点に注意してください[…]

#### タスク 3 - Graph API を使用してチームを作成する

このタスクでは、組織の自動化計画に向けて Teams で Graph API の機能をテストします。最小設定で **Early Adopters** という新しいチームを作成します[…]

1. 提供された資格情報で **Client 1 VM** に接続します。

2. Microsoft Edge を開きブラウザーを最大化し、**Graph Explorer**（[https://developer.microsoft.com/graph/graph-explorer](https://developer.microsoft.com/graph/graph-explorer)）に移動します。

3. ページ左側の **Sign in to Graph Explorer** を選択し、**Joni Sherman**（JoniS@&lt;YourTenant&gt;.onmicrosoft.com）としてサインインします。

4. 初めて Graph Explorer にアクセスする場合、**Permissions requested** ページが表示されます。**承諾 (Accept)** を選択します。

5. **GET** ボタンを選択し、ドロップダウンから **POST** を選択します。

6. 中央の **v1.0** は変更しません。

7. **Run query** ボタンの前のテキスト ボックスに次を入力します:

   - [https://graph.microsoft.com/v1.0/teams](https://graph.microsoft.com/v1.0/teams)

8. 上部ペインで **Modify permissions (Preview)** を選択します。

   ![Graphical user interface, text, application, email Description automatically generated](media/MS-700-lab_M03_ak_image1.png)

9. 右にスクロールし、**Team.Create** の **Consent** ボタンを選択します。

10. 再度 **Permissions requested** ページが表示されたら **承諾 (Accept)** を選択します。

11. Microsoft Developers サイトにリダイレクトされた場合は、**Graph Explorer**（[https://developer.microsoft.com/graph/graph-explorer](https://developer.microsoft.com/graph/gra[…]）に戻ります。

12. **Request body** タブを選択し、次のコードを入力します:

    ```json
	{

	"template@odata.bind":"https://graph.microsoft.com/v1.0/teamsTemplates('standard')",

	"displayName": "Early Adopters",

	"description": "The Early Adopters Workspace.",

	"visibility": "Public" 

	}
	```

13. 右上の **Run query** を選択します。

14. しばらくすると、要求本文ウィンドウの下に緑色のバーでチェック マークと **Accepted** のメッセージが表示されます。

15. さきほどの **Request body** テキスト ボックスの内容をすべて削除し、次の内容に置き換えます:

    ```json
	{

	"template@odata.bind": "https://graph.microsoft.com/v1.0/teamsTemplates('standard')",

	"visibility": "Public",

	"displayName": "Tech Meetings",

	"description": "Space for all employees participating in the champions program, who want exchange each other about the newest features.",

	"channels": [

	{

	"displayName": "Welcome Hall",

	"isFavoriteByDefault": true,

	"description": "Channel for introducing yourself as a member of the tech meeting participants."

	},

	{

	"displayName": "Tech Lunch and Dinner",

	"isFavoriteByDefault": true,

	"description": "When will be the next tech lunch and who has any suggestions where to meet."

	},

	{

	"displayName": "Q and A",

	"description": "Questions and answers: Teams users giving a helping hand to other users.",

	"isFavoriteByDefault": true

	},

	{

	"displayName": "Issues and Feedback 🐞",

	"description": "Leave some feedback for the IT-Staff.",

	"isFavoriteByDefault": false

	}

	],

	"memberSettings": {

	"allowCreateUpdateChannels": true,

	"allowDeleteChannels": false,

	"allowAddRemoveApps": true,

	"allowCreateUpdateRemoveTabs": true,

	"allowCreateUpdateRemoveConnectors": true

	},

	"guestSettings": {

	"allowCreateUpdateChannels": true,

	"allowDeleteChannels": false

	},

	"funSettings": {

	"allowGiphy": true,

	"giphyContentRating": "Moderate",

	"allowStickersAndMemes": true,

	"allowCustomMemes": true

	},

	"messagingSettings": {

	"allowUserEditMessages": true,

	"allowUserDeleteMessages": true,

	"allowOwnerDeleteMessages": true,

	"allowTeamMentions": true,

	"allowChannelMentions": true

	},

	"discoverySettings": {

	"showInTeamsSearchAndSuggestions": true

	}

	}
	```

16. 右上の **Run query** を選択します。

17. しばらくすると、再びチェック マークと **Accepted** を含む緑色のバーが表示されます。

18. Teams デスクトップ アプリを開きます。左ペインで **Teams** を選択し、新たに作成された **“Early Adopters”** と **“Tech Meetings”** を確認します。

Graph API を使って 2 つのチームを作成できました。Graph の機能テストは完了です。次の演習に進みます。

#### タスク 4 – チームをアーカイブ/アーカイブ解除する

このラボでさまざまなチームを作成した後、チームを削除するさまざまな方法も評価する必要があります。このタスクでは、アーカイブ機能をテストし、Sales チームを[…]

1. **Client 1 VM** に接続し、**Joni Sherman**（JoniS@&lt;YourTenant&gt;.onmicrosoft.com）として **Teams デスクトップ クライアント** を開きます。

2. 左ペインで **Teams** を選択し、Teams の横の **…** を選んで **自分のチームとチャネル** をクリックします。

3. **Sales** チームをアーカイブします

   1. **Sales** チームの左のチェック マークを選択し、上部ペインから **アーカイブ** を選択します。
   2. **チーム メンバーに対して SharePoint サイトを読み取り専用にする** のチェック ボックスをオンにして **アーカイブ** を選択します。
   3. **状態** 列がオレンジ色の **アーカイブ済み** に変わります。ブラウザーは開いたまま進みます。**Sales** チームで問題がある場合は、他のチームをアーカイブしてください（…）

4. アーカイブ済みチームを確認します

   1. **Client 2 VM** に接続し、**Lynne Robbins**（LynneR@&lt;YourTenant&gt;.onmic[…]）として [**Microsoft Teams Web クライアント (https://teams.microsoft.com/)**](https://teams.microsoft.com/) にアクセスします。
   2. Teams を選択し、**Teams とチャネル** を選択します。
   3. **アーカイブ** セクションを展開し、**Sales** チームを選択します。**隠しチーム** セクションの下に **Sales** チームが表示されます。
   4. **Sales** チームの **一般** チャネルを選択し、**新しい会話** が使用できないことを確認します。

5. **Sales** チームをアーカイブ解除します

   1. 再度 **Client 1 VM** に接続し、**Joni Sherman** として Teams 管理センターにアクセスします。
   2. **Sales** の左のチェック ボックスを再度選択し、上部メニューから **アーカイブを解除** を選択します。**状態** が **アクティブ** に戻ります。

6. アーカイブ解除したチームを確認します

   1. **Client 2 VM** に接続し、**Lynne Robbins**（LynneR@&lt;YourTenant&gt;.onmic[…]）として [**Microsoft Teams Web クライアント (https://teams.microsoft.com/)**](https://teams.microsoft.com/) にアクセスします。
   2. 左側で **Teams** を選択します。
   3. しばらくすると、**Sales** チームと **一般** チャネルの文字色が元に戻りますが、チームは非表示のままです。
   4. Sales チーム名の右側の三点リーダー（…）を選択し、**表示** を選択します。

7. ブラウザーは開いたまま、サインイン状態を維持します。

アーカイブ機能をテストし、アーカイブ済みチームの制限を確認できました。これは、コンプライアンス保全のためのアーカイブ機能テストの最初の要件を満たします[…]

#### タスク 5 - チームを削除して復元する

このタスクでは、前のレッスンで作成したチームの 1 つを削除し、復元方法を学びます。

1. **Client 2 VM** に接続し、**Lynne Robbins**（LynneR@&lt;YourTenant&gt;.onmicr[…]）として [**Microsoft Teams Web クライアント (https://teams.microsoft.com/)**](https://teams.microsoft.com/) にアクセスします。

2. Teams Web クライアントの左ナビゲーションで、**Sales** チーム名の右の三点リーダー（…）を選択し、一覧から **チームの削除** を選択します。

3. **Sales チームを削除** で、**すべてが削除されることを理解しました** にチェックを入れ、**チームの削除** を選択します。

4. グループを復元します

   1. **Client1 VM** に接続し、**MOD Administrator** として Entra 管理センター（https://entra.microsoft.com/）にアクセスします。
   2. 左ナビゲーションで **ID** > **グループ** を選択します。
   3. **グループ** ページで、左側の **削除済みのグループ** を選択します。
   4. すべての削除済みグループが表示され、その中に **Sales** グループがあります。
   5. **Sales** グループの左のチェック ボックスを選択し、上部ペインの **グループの復元** を選択します。**削除済みグループを復元しますか** のダイアログで **はい** を選択して確定します。

5. 復元されたグループを確認します。

   1. **Client 2 VM** に接続し、**Lynne Robbins**（LynneR@&lt;YourTenant&gt;.onmicroso[…]）として [**Microsoft Teams Web クライアント (https://teams.microsoft.com/)**](https://teams.microsoft.com/) にアクセスします。
   2. **Sales** チームが再びチーム一覧に表示されます。必要に応じて **F5** でページを更新します。
   3. チーム名の右の三点リーダー（…）を選択し、**チームの管理** を選択します。**メンバー** タブに所有者とすべてのメンバーが再表示されます。

**注:** チームの削除から復元までの全プロセスには最大 24 時間かかる場合があります。すぐに表示されない場合は、このラボの後半で再度確認してください。

Teams Web クライアントでチームを削除し、Azure ポータルで復元できました。

#### タスク 6 - 動的メンバーシップでチーム メンバーを管理する

Contoso はカナダに進出し、トロントに新しいオフィスを開設します。システム管理者として、Office 365 サービスの場所に基づく動的グループを構成する必要があります。

1. **Client1 VM** に接続し、**MOD Administrator** として Entra 管理センター（https://entra.microsoft.com/）にアクセスします。

2. 左ナビゲーションで **ID** > **グループ** > **すべてのグループ** を選択します。

3. **グループ | すべてのグループ** ページで **CA-Office** グループを検索して選択します。

4. **CA-Office** ページの左ナビゲーションで **プロパティ** を選択します。

5. **メンバーシップの種類** を **割り当て済み** から **動的ユーザー** に変更します。

6. **動的ユーザー メンバー** の下で **動的クエリの追加** を選択します。

7. **動的メンバーシップ ルール** ページで、次の情報を入力します:

   - プロパティ: **accountEnabled**
   - 演算子: **等しい**
   - 値: **true**

8. **+ 式を追加** を選択し、次の情報を入力します:

   - プロパティ: **usageLocation**
   - 演算子: **等しい**
   - 値: **CA**

9. **保存** を 2 回選択します。

   メンバーシップが新しい動的メンバーシップ ルールに従って変更されるという警告が表示されます。**はい** を選択して確定します。

11. **CA-Office** グループ ウィンドウの左ナビゲーションで **概要** を選択します。

12. 概要ウィンドウで **動的ルールの処理状態** を確認します。

   状態が **成功** と表示されるまで待ち、ブラウザーを更新します。反映には数分かかる場合があります。

13. 次に左ナビゲーションの **メンバー** を選択し、**最新の情報に更新** を選択します。**Alex Wilber** がメンバー一覧に含まれ、**Allan Deyoung** がグループから削除されていることを確認します[…]

14. 左ナビゲーションの **所有者** を選択し、Joni が動的グループ条件に合致しなくても引き続きグループの所有者であることを確認します。

Microsoft 365 グループを静的（割り当て）から動的メンバー���ップに変換できました。メンバーシップはユーザーの usageLocation とアカウント有効状態で制御されます。条件に合致する新規ユーザーは自動的に追加されます[…]

### **演習 2: チャネルとメッセージのポリシーを構成する**

この演習では、新しいプライベート チャネルの作成と、ユーザーがチャットで使用できるツールを管理するためのポリシーを構成します。

#### タスク 1 - giphy、ミーム、ステッカー用のメッセージング ポリシーを作成する

会社は Teams のコミュニケーションにおけるグラフィック要素の使用を制限したいと考えています。Teams サービス管理者として、パイロット ユーザーが会話で GIF ファイルやミーム、ステッカーを使用できないようにする新しいメッセージ ポリシーを作成します[…]

1. **Client 1 VM** に接続し、**Joni Sherman**（JoniS@&lt;YourTenant&gt;.onmicrosoft.com）として Teams 管理センター（https://admin.teams.microsoft.com）にアクセスします。

2. Teams 管理センターの左ナビゲーションで **メッセージング** > **メッセージング ポリシー** を選択します。 

3. **ポリシーの管理** タブで **+ 追加** を選び、次を入力します

   - **名前**: Regular users without fun stuff
   - **説明**: 会話での giphy、ステッカー、ミームを無効にするポリシー
   - **会話での Giphys**: オフ
   - **会話でのミーム**: オフ
   - **会話でのステッカー**: オフ
   - 残りは既定のまま。**保存** を選択。

4. **メッセージング ポリシー** の概要ページに戻り、**Regular users without fun stuff** の左のチェックを選択してから **ユーザーの割り当て** を選択します。 

   **注:** **ユーザーの割り当て** が見えない場合は **ユーザーの管理** を選んでメニューを展開します。

5. 次のパイロット ユーザーを検索して **追加** を選択します。その後 **適用**、プロンプトが出たら **確認** を選択します。

   - **Alex Wilber**
   - **Lynne Robbins**
   - **Diego Siciliani**

**注:** 設定が反映されるまで最大 24 時間かかる場合があります。

このタスクでは、新しいメッセージング ポリシーを構成し、パイロット ユーザーに割り当てました。ポリシーが有効になるまで時間をおいて、次のタスクに進みます。

#### タスク 2 - チーム内のプライベート チャネルを管理する

Contoso の Teams 管理者として��Sales チームに一部のメンバーのみがアクセスできる **confidential** というプライベート チャネルを作成します。

1. **Client 1 VM** に接続し、**Joni Sherman**（JoniS@&lt;YourTenant&gt;.onmicrosoft.com）として Teams 管理センター（https://admin.teams.microsoft.com）にアクセスします。

2. 左ナビゲーションで **チーム** > **チームの管理** を選択します。

3. **Sales** チームを選択し、**チャネル** タブを選択します。

4. プライベート チャネルを追加します

   1. 上部メニューの **+ 追加** を選択します。
   2. **追加** ウィンドウで次を入力します:
      - **名前**: Confidential sales
      - **説明**: 機密のプライベート Sales チャネル
      - **種類**: プライベート
      - **チャネル所有者**: Lynne Robbins

3. **適用** を選択します。

5. プライベート チャネルを確認します

   1. **Client 2 VM** に接続し、**Lynne Robbins**（LynneR@&lt;YourTenant&gt;.onmicrosoft.com）として **Teams Web クライアント**（[(https://teams.microsoft.com)](https://teams.microsoft.com/)）にアクセスします[…]
   2. **Teams** を選択すると、小さな鍵アイコン付きで新しいプライベート チャネル **Confidential sales** が表示されます。

このタスクでは、Microsoft Teams 管理センターでプライベート チャネルを作成し、アクセスを構成・確認する方法を学びました。

### **演習 3: アプリ設定を管理する**

#### タスク 1 - サードパーティ ストレージ プロバイダーを無効にする

過去にユーザーはサードパーティのストレージ プロバイダーを含むさまざまな場所にデータを保存していました。最近、会社は全ユーザーに OneDrive を展開し、ユーザーが SharePoint[…]

1. **Client 1 VM** に接続し、**Joni Sherman**（JoniS@&lt;YourTenant&gt;.onmicrosoft.com）として Teams 管理センター（https://admin.teams.microsoft.com）にアクセスします。

2. 左ナビゲーションで **チーム** > **Teams の設定** を選択します。

3. **Teams の設定** ページで **ファイル** セクションに移動します。

4. 次のファイル共有とクラウド ファイル ストレージ オプションを構成します。

   - **Citrix Files:** オフ
   - **Dropbox:** オフ
   - **Box:** オン
   - **Google Drive:** オフ
   - **Egnyte:** オフ

5. 下までスクロールし **保存** を選択します。

**注:** 設定が反映されるまで最大 24 時間かかる場合があります。

このタスクでは、テナント全体でサードパーティ ストレージ プロバイダーを有効/無効にする方法を学びました。

#### タスク 2 - 組織レベルでアプリをブロックする

このタスクでは、テナント全体で Google Analytics アプリをブロックします。

1. **Client 1 VM** に接続し、**Joni Sherman**（JoniS@&lt;YourTenant&gt;.onmicrosoft.com）として Teams 管理センター（https://admin.teams.microsoft.com）にアクセスします。

2. Teams 管理センターの左ナビゲーションで **Teams アプリ** > **アプリの管理** を選択します。

3. **アプリの管理** ページで検索ボックスに **Google** と入力します。 

   ![Graphical user interface, application Description automatically generated](media/MS-700-lab_M03_ak_image5.png)

4. 検索結果で **Google Analytics** を選択して開きます。

5. 画面左上の **操作** ドロップダウンを選択し、**アプリをブロック** を選択します。

**注:** 設定が反映されるまで最大 24 時間かかる場合があります。

このタスクでは、テナントで Google Analytics アプリをブロックする方法を学びました。

### **演習 4: アプリの設定ポリシーを作成/管理する**

Teams 管理者として、ユーザーにとって最も重要なアプリを強調表示し、サードパーティや社内開発のアプリを含む、組織のユーザーが必要とするアプリを紹介する必要があります[…]

#### タスク 1 - 既定の組織全体のアプリ ポリシーを編集する

パイロット プロジェクトでは、すべてのユーザーの既定アプリとして **Planner と To Do のタスク (Tasks by Planner and To Do)** を追加したいと考えています。そのため、既定の組織全体のアプリ ポリシーを編集します。この反映には時間がかかる場合があります[…]

1. **Client 1 VM** に接続し、**Joni Sherman**（JoniS@&lt;YourTenant&gt;.onmicrosoft.com）として Teams 管理センター（https://admin.teams.microsoft.com）にアクセスします。

2. 左ナビゲーションで **Teams アプリ** > **アプリの設定ポリシー** を選択します。

3. **アプリの設定ポリシー** ページの **ポリシーの管理** から **Global (組織全体の既定)** を選択して、組織全体のアプリ ポリシーを開きます。

4. **ピン留めされたアプリ** セクションで **アプリを追加** を選択します。

5. **インストール済みアプリの追加** ページで、検索ボックスに **Planner** と入力し、アプリ名にマウスオーバーして **追加** を 2 回選択します。

6. **Planner** が **ピン留めされたアプリ** セクションに表示されていることを確認し、**保存**、**確認** を選択します。

**注:** 設定が反映されるまで最大 24 時間かかる場合があります。

このタスクでは、Microsoft Teams 管理センターから既定アプリをピン留めする方法を学びました。

#### タスク 2 - カスタムのアプリの設定ポリシーを作成する

1. **Client 1 VM** に接続し、**Joni Sherman**（[**JoniS@&lt;YourTenant&gt;.onmicrosoft.com**](mailto:JoniS@&lt;YourTena[…)) として Teams 管理センター（**https://admin.teams.microsoft.com**）にアクセスします。

2. Microsoft Teams 管理センターの左ナビゲーションで **Teams アプリ** > **アプリの設定ポリシー** に移動します。

3. **+ 追加** を選択します。 

4. 次の情報を入力します

   - 名前: **Sales team**
   - 説明: **Adobe Acrobat Sign をインストールし、Viva Goals をピン留めする。**
   - ユーザーによるピン留め: **オン**
   - ユーザーにアプリをインストールする:
     1. **インストール済みアプリ** で **アプリを追加** を選択。
     2. **インストール済みアプリの追加** ペインで、ユーザーが Teams を開始したときに自動インストールさせたいアプリを検索。  
        この演習では **Adobe** を検索し、**Adobe Acrobat Sign** を選択して **追加** を選び、**追加するアプリ** 一覧に入れます。  
        その後 **追加** を選び、**インストール済みアプリ** に追加を完了します。
   - アプリをピン留めする:
     1. **ピン留めされたアプリ** で **アプリを追加** を選択。
     2. **ピン留めするアプリの追加** ペインで **Viva Goals** を検索し、**追加** を選択。
     3. **保存** を選択。

5. **保存** を選択します。

新しいカスタム アプリの設定ポリシーを作成しました。

#### タスク 3 - カスタムのアプリの設定ポリシーをユーザーに割り当てる

1. **Microsoft Teams 管理センター** の左ナビゲーションで **Teams アプリ** > **アプリの設定ポリシー** に移動します。

2. **Sales team** アプリの設定ポリシーを選択します。

3. **ユーザーの割り当て** を選択します。

4. **ユーザーの管理** ペインで **Alex Wilber** を検索して **追加** を選択します。

5. **適用** を選択します。

### **演習 5: 構成したポリシー設定をテストする**

この演習では、影響を受けるユーザー **Lynne Robbins** のクライアントで構成済みポリシー設定をテストし、**Joni Sherman** の利用可能なクライアント設定と比較します。

#### タスク 1 – メッセージング ポリシーとプライベート チャネル アクセスをテストする

このタスクでは、演習 1 で構成した **メッセージング ポリシー** をテストし、影響を受けるユーザー（Lynne Robbins）と通常ユーザー（Joni Sherman）の違いを確認します。

1. **Client 2 VM** に接続し、**Lynne Robbins**（LynneR@&lt;YourTenant&gt;.onmicroso[…]）として [**Microsoft Teams Web クライアント (https://teams.microsoft.com/)**](https://teams.microsoft.com/) にアクセスします。

2. 左ナビゲーションで **チャット** > **新しいチャット** アイコンを選択します。

   ![Graphical user interface, application Description automatically generated with medium confidence](media/MS-700-lab_M03_ak_image8.png)

3. メイン ペインで **Joni Sherman** を入力して会話を開始します。

4. **giphy**、**ミーム**、**ステッカー** のアイコンが表示されないことに気づきます。

#### タスク 2 – ブロックされたアプリとストレージ プロバイダーをテストする

このタスクでは、ブロックされたアプリをテストします。

1. **Client 2 VM** に接続し、**Lynne Robbins**（LynneR@&lt;YourTenant&gt;.onmicroso[…]）として [**Microsoft Teams Web クライアント (https://teams.microsoft.com/)**](https://teams.microsoft.com/) にアクセスします。

2. 左ナビゲーションで **アプリ** を選択します。

3. 検索ボックスで **Google** を検索します。

4. 検索結果で **Google Analytics** を選択します。鍵アイコンと「リクエスト」ボタンが表示されていることを確認します。 

5. 左ナビゲーションで **チャット** を選択し、**Sales** チームの **sales** チャネルに移動します。

6. **ファイル** タブを選択し、リボンの **…** を選択します。

7. **OneDrive にショートカットを追加** を選択します。

8. Teams からサインアウトし、開いているウィンドウをすべて閉じます。

END OF LAB
