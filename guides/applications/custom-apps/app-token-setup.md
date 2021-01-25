---
rank: 3
type: guide
hide_step_number: false
related_endpoints: []
related_guides:
  - authentication/select
  - authentication/oauth2
  - applications/custom-apps/app-approval
required_guides:
  - authentication/select
  - applications/custom-apps
related_resources: []
alias_paths:
  - /guides/applications/limited-access-apps
category_id: applications
subcategory_id: applications/custom-apps
is_index: false
id: applications/custom-apps/app-token-setup
total_steps: 4
sibling_id: applications/custom-apps
parent_id: applications/custom-apps
next_page_id: applications/custom-apps/app-approval
previous_page_id: applications/custom-apps/jwt-setup
source_url: >-
  https://github.com/box/developer.box.com/blob/main/content/guides/applications/custom-apps/app-token-setup.md
fullyTranslated: true
---
# アプリトークンを使用した設定

カスタムアプリは、認証にサーバー側の[アプリトークン][app-token]を使用するよう設定できます。

<CTA to="g://authentication/app-token">

アプリトークン認証のしくみを確認する

</CTA>

## 前提条件

サーバー側認証を使用してカスタムアプリを設定するには、Box Enterpriseアカウントから[開発者コンソール][devconsole]にアクセスできることを確認する必要があります。または、[Developerアカウント][devaccount]にサインアップすることもできます。

## アプリの作成手順

### 1. 開発者コンソールにログインする

Boxにログインし、[開発者コンソール][devconsole]に移動して、\[**アプリの新規作成**] を選択します。

### 2. カスタムアプリを作成する

アプリケーションの種類のリストから \[**アクセス制限付きアプリ**] を選択します。次の手順を促すモーダルが表示されます。

<ImageFrame border>

![アプリケーションの選択画面](../images/select-app-type.png)

</ImageFrame>

### 3. アプリ名を選択する

最後に、アプリケーションの一意の名前を選択し、\[**アプリの作成**] をクリックします。

<ImageFrame border width="600" center>

![アプリ名のフォーム](../images/limited-access-naming.png)

</ImageFrame>

## アプリの承認

キーペアがアプリケーションに正常に追加されたら、Box Enterprise管理者はBox管理コンソール内でこのアプリケーションを承認する必要があります。

\<C1>開発者コンソール\</c1>内でアプリケーションの \[**一般設定**] タブに移動し、\[**アプリの承認**] セクションまで下にスクロールします。

<ImageFrame border width="400" center>

![キーの追加と管理](../images/app-authorization.png)

</ImageFrame>

\[**確認して送信**] をクリックして、承認を得るためにBox Enterprise管理者にメールを送信します。このプロセスの詳細については、[アプリの承認に関するサポート記事][app-auth]を参照してください。

## 基本的な構成

アプリケーションを使用するには、事前にいくつかの基本的な追加構成が必要になる場合があります。

### プライマリおよびセカンダリアプリトークン

アクセス制限付きアプリでの認証は、あらかじめ構成された[アプリトークン][app-token]を使用して行われます。アプリトークンを構成するには、[開発者コンソール][devconsole]内でアプリケーションの \[**構成**] タブに移動します。

\[\<C0>プライマリアクセストークン\</c0>] セクションまで下にスクロールし、\[**キーを生成**] ボタンをクリックします。

<ImageFrame border width="600" center>

![アプリトークンの作成](../images/app-generate-key.png)

</ImageFrame>

アプリトークンは、自動的に期限切れになるよう構成することも、有効期限なしで構成することもできます。作成後は、このキーを使用して[API呼び出し][api-calls]を実行できます。

<Message warning>

# アプリの承認

アプリトークンは、Box管理コンソール内でアプリケーションの承認が成功するまで生成できません。

</Message>

### CORSドメイン

アプリケーションがJavaScriptでフロントエンドのブラウザコードからAPI呼び出しを実行する場合は、[クロスオリジンリソース共有][cors] (CORS) のために、これらの呼び出しの実行元となるドメインを許可リストに追加する必要があります。すべてのリクエストがサーバー側のコードから発行される場合は、このセクションをスキップできます。

許可リストに完全なURIを追加するには、[開発者コンソール][devconsole]の \[**構成**] タブの下部にある \[**CORSドメイン**] セクションに移動します。

<ImageFrame border>

![アプリ名のフォーム](../images/app-cors.png)

</ImageFrame>

[devconsole]: https://app.box.com/developers/console

[devaccount]: https://account.box.com/signup/n/developer

[devtoken]: g://authentication/access-tokens/developer-tokens

[scopes]: g://api-calls/permissions-and-errors/scopes

[cors]: https://en.wikipedia.org/wiki/Cross-origin_resource_sharing

[app-token]: g://authentication/app-token

[api-calls]: g://api-calls

[app-auth]: https://community.box.com/t5/Managing-Developer-Sandboxes/Authorizing-Apps-in-the-Box-App-Approval-Process/ta-p/77293
