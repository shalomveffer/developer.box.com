---
rank: 2
related_endpoints: []
related_guides:
  - authentication/jwt
required_guides:
  - authentication/select
  - applications/custom-apps
  - applications/custom-apps/app-approval
related_resources: []
alias_paths:
  - /docs/setting-up-a-jwt-app
  - /docs/authentication-with-jwt
  - /docs/app-auth
category_id: applications
subcategory_id: applications/custom-apps
is_index: false
id: applications/custom-apps/jwt-setup
type: guide
total_steps: 4
sibling_id: applications/custom-apps
parent_id: applications/custom-apps
next_page_id: applications/custom-apps/app-token-setup
previous_page_id: applications/custom-apps
source_url: >-
  https://github.com/box/developer.box.com/blob/main/content/guides/applications/custom-apps/jwt-setup.md
fullyTranslated: true
---
# JWTを使用した設定

カスタムアプリは、[JWT][jwt]によるサーバー側認証を使用するよう設定できます。

<CTA to="g://authentication/jwt">

JWT認証のしくみを確認する

</CTA>

## 前提条件

サーバー側認証を使用してカスタムアプリを設定するには、Box Enterpriseアカウントから[開発者コンソール][devconsole]にアクセスできることを確認する必要があります。または、[Developerアカウント][devaccount]にサインアップすることもできます。

## アプリの作成手順

### 1. 開発者コンソールに移動する

Boxにログインし、[開発者コンソール][devconsole]に移動して、\[**アプリの新規作成**] を選択します。

### 2. アプリケーションの種類を選択する

アプリケーションの種類のリストから \[**カスタムアプリ**] を選択します。次の手順を促すモーダルが表示されます。

<ImageFrame border center>

![認証の選択画面](../images/select-app-type.png)

</ImageFrame>

### 3. 認証の種類とアプリ名を選択する

[キーペアを使用][kp]してアプリケーションIDを確認する場合は、\[**サーバー認証 (JWT使用)**] を選択します。[クライアントIDとクライアントシークレットを使用][ccg]してアプリケーションIDを確認する場合は、\[**サーバー認証 (クライアント資格情報の許可)**] を選択します。その後、アプリケーションの名前を入力し、\[**アプリの作成**] をクリックします。

<Message warning>

選択すると、新しいアプリケーションを作成しない限り、別の認証方式に変更できません。

</Message>

<ImageFrame border width="600" center>

![アプリ名のフォーム](../images/jwt-three-options.png)

</ImageFrame>

## 公開キーと秘密キーのペア

<Message>

このセクションは、認証方式として \[サーバー認証 (クライアント資格情報の許可)] を選択した場合はスキップできます。

</Message>

\[サーバー認証 (JWT使用)] を利用してカスタムアプリを作成すると、[開発者コンソール][devconsole]の \[構成] タブでキーペアを生成できます。また、独自のキーペアを生成して、その公開キーをBoxに提供することもできます。選択する方法に関係なく、セキュリティの目的で、Boxアカウントでは[2FA][2fa]を有効にしておく必要があります。

### キーペアの生成(推奨)

Boxで生成されたキーペアを使用する場合は、[開発者コンソール][devconsole]に移動し、そこで構成ファイルを生成できます。このファイルには、公開/秘密キーペアのほか、認証に必要なその他さまざまなアプリケーションの詳細が含まれています。

このファイルを生成するには、[開発者コンソール][devconsole]の \[**構成**] タブに移動し、\[**公開キーの追加と管理**] セクションまで下にスクロールします。

<ImageFrame border width="600" center>

![キーの追加と管理](../images/app-add-keys.png)

</ImageFrame>

\[\<C0>公開/秘密キーペアを生成\</c0>] ボタンをクリックすると、Boxによってキーペアが生成されます。これにより、アプリケーションコードに移すことができるJSON構成ファイルのダウンロードが開始されます。

<Message danger>

セキュリティ上の理由により、Boxには秘密キーが保存されません。秘密キーを紛失した場合は、キーペア全体のリセットが必要になります。

</Message>

### 手動によるキーペアの追加

代わりに、独自のキーペアを生成し、その公開キーを[開発者コンソール][devconsole]にアップロードすることもできます。

OpenSSLを使用してキーペアを作成するには、ターミナルウィンドウを開き、以下のコマンドを実行します。

```shell
openssl genrsa -des3 -out private.pem 2048
openssl rsa -in private.pem -outform PEM -pubout -out public.pem
```

<Message>

# Windowsシステムの場合

Windowsユーザーは、[Cygwin][cygwin]パッケージをインストールして使用することで、OpenSSLを実行できます。

</Message>

その後、[開発者コンソール][devconsole]でアプリケーションの \[構成] タブに移動し、\[**公開キーの追加と管理**] セクションまで下にスクロールします。

<ImageFrame border width="600" center>

![キーの追加と管理](../images/app-add-keys.png)

</ImageFrame>

\[\<C0>公開キーを追加\</c0>] ボタンをクリックし、上記の手順で生成された公開キーを入力して、\[**確認して保存**] をクリックします。

## アプリの承認

アプリケーションを使用するには、Box管理者がBox管理コンソールでそのアプリケーションを承認しておく必要があります。

[開発者コンソール][devconsole]内でアプリケーションの \[**一般設定**] タブに移動し、\[**アプリの承認**] セクションまで下にスクロールします。

<ImageFrame border width="400" center>

![キーの追加と管理](../images/app-authorization.png)

</ImageFrame>

\[**確認して送信**] をクリックして、承認を得るためにBox Enterprise管理者にメールを送信します。このプロセスの詳細については、[アプリの承認に関するサポート記事][app-auth]を参照してください。

### 構成変更後の再承認

一般的な経験則では、開発者コンソールで構成を変更した後は、Box管理コンソールでアプリケーションの再承認が必要になります。この手順をスキップすると、生成されたどのアクセストークンにも、構成の変更が反映されません。

## 基本的な構成

### アプリケーションアクセス

デフォルトでは、アプリケーションで正常に操作できるのは、そのアプリケーションのデータと[App User][user-types]のデータのみです。会社の既存の管理対象ユーザーも操作するには、[開発者コンソール][devconsole]の \[**構成**] タブからアクセスできる \[**アプリケーションアクセス**] 設定に移動し、\[**Enterprise**] に設定します。 

<ImageFrame border>

![アプリのアクセスレベル](../images/app-access-level.png)

</ImageFrame>

### アプリケーションスコープ

スコープを使用して、アプリケーションがデータにアクセスするために必要な権限を定義します。各オプションの詳細については、[スコープのガイド][scopes]を参照してください。

<ImageFrame border width="600" center>

![アプリスコープ](../images/app-scopes.png)

</ImageFrame>

### CORSドメイン

アプリケーションがJavaScriptでフロントエンドのブラウザコードからAPI呼び出しを実行する場合は、[クロスオリジンリソース共有][cors] (CORS) のために、これらの呼び出しの実行元となるドメインを許可リストに追加する必要があります。すべてのリクエストがサーバー側のコードから発行される場合は、このセクションをスキップできます。

許可リストに完全なURIを追加するには、[開発者コンソール][devconsole]の \[**構成**] タブの下部にある \[**CORSドメイン**] セクションに移動します。

<ImageFrame border>

![アプリのCORS設定](../images/app-cors.png)

</ImageFrame>

[devconsole]: https://app.box.com/developers/console

[devaccount]: https://account.box.com/signup/n/developer

[devtoken]: g://authentication/access-tokens/developer-tokens

[scopes]: g://api-calls/permissions-and-errors/scopes

[cors]: https://en.wikipedia.org/wiki/Cross-origin_resource_sharing

[user-types]: g://authentication/user-types

[cygwin]: http://www.cygwin.com/

[app-auth]: https://community.box.com/t5/Managing-Developer-Sandboxes/Authorizing-Apps-in-the-Box-App-Approval-Process/ta-p/77293

[jwt]: g://authentication/jwt

[2fa]: https://support.box.com/hc/en-us/articles/360043697154-Two-Factor-Authentication-Set-Up-for-Your-Account

[kp]: g://authentication/jwt/without-sdk/#public-and-private-key-pair

[ccg]: g//authentication/jwt/without-sdk/#client-credentials-grant
