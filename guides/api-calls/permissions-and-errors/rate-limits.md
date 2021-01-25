---
rank: 2
related_endpoints:
  - get_search
  - put_files_content
related_guides:
  - api-calls/permissions-and-errors/common-errors
related_resources:
  - client_error
required_guides: []
alias_paths: []
category_id: api-calls
subcategory_id: api-calls/permissions-and-errors
is_index: false
id: api-calls/permissions-and-errors/rate-limits
type: guide
total_steps: 4
sibling_id: api-calls/permissions-and-errors
parent_id: api-calls/permissions-and-errors
next_page_id: api-calls/permissions-and-errors/scopes
previous_page_id: api-calls/permissions-and-errors/common-errors
source_url: >-
  https://github.com/box/developer.box.com/blob/main/content/guides/api-calls/permissions-and-errors/rate-limits.md
fullyTranslated: true
---
# レート制限

There are three common types of API call rate limitations that Box may use at its discretion to best protect network resources and preserve the quality of our customer experience.

## User based

These rate limits protect our service from issues that may arise when a single user generates too much traffic. The number of API calls that a user can make in a minute is limited as described below. These limits apply to all Box user accounts and are the most common. Generally, they are initiated when a user exceeds approximately 1000 API/calls/minute, but certain API endpoints may have different rate limits.

## Quality of service

These rate limits are designed to protect the quality of service of our infrastructure. If there is resource contention in the infrastructure, we introduce automatic rate limits to prevent system degradation and outages. For instance, if an application happens to be accessing the same physical database server, such as the use of a file migration tool accessing related resources that access the same underlying physical resources, Box may impose temporary rate-limits when load spikes and adjust them as the system recovers.

## Licensing based

All Box Business Plans come with a licensed number of permitted API calls per enterprise per month. These license based rate limits are designed to prevent excessive overages and misuse of network resources. If Box's infrastructure detects that a tool used by or on behalf of a customer has exceeded that customer's API license allocation or is intending to circumvent network controls, additional selective rate-limiting may be imposed. You can see the default API allocations licensed with a particular account level at our [pricing page][pricing], but note that some customers purchase Platform API Pricing plans that increase their allocation.

## APIごとのレート制限

現在、Box APIにはいくつかの異なるレート制限があります。

* 一般的なAPI呼び出し
  * 1ユーザーあたりのAPIリクエストは1000件/分
* アップロード
  * 1ユーザーあたりのファイルアップロードリクエストは240件/分
* 検索
  * [検索エンドポイント][search]に対して、1ユーザーあたりの検索数は6件/秒
  * 基本のレート制限に加えてさらに2つの制限が適用されます
    * 1ユーザーあたりの検索数は60件/分
    * 会社あたりの検索数は12件/秒

## レート制限エラー

アプリケーションがレート制限に達すると、APIは、HTTPステータスコードが`429 Too Many Requests`のAPI応答を返します。

応答には以下のヘッダーとJSON本文が含まれます。

```yaml
retry-after: 100
```

```json
{
  "type": "error",
  "status": 429,
  "code": "rate_limit_exceeded",
  "help_url": "http://developers.box.com/docs/#errors",
  "message": "Request rate limit exceeded, please try again later",
  "request_id": "abcdef123456"
}
```

詳細については、[クライアントエラーのリソース](resource://client_error)を参照してください。

<Message type="notice">

`retry-after`ヘッダーでは、次のAPI呼び出しが再試行可能になるまで待機する秒数を指示します。一般的には、API呼び出しの再試行に指数バックオフ戦略を使用することをお勧めします。

</Message>

[search]: e://get_search

[pricing]: https://www.box.com/pricing
