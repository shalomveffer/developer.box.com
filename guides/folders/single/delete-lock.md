---
rank: 10
related_endpoints:
  - delete_folder_locks_id
related_guides:
  - folders/single/create-lock
  - folders/single/get-locks
alias_paths: []
related_resources:
  - folder_locks
category_id: folders
subcategory_id: folders/single
is_index: false
id: folders/single/delete-lock
type: guide
total_steps: 10
sibling_id: folders/single
parent_id: folders/single
next_page_id: ''
previous_page_id: folders/single/get-locks
source_url: >-
  https://github.com/box/developer.box.com/blob/main/content/guides/folders/single/delete-lock.md
fullyTranslated: true
---
# フォルダのロックの削除

Box内のフォルダに適用されたロックを削除するには、フォルダのロックIDを指定して`DELETE /folder_locks/:id` APIを呼び出します。

<Samples id="delete_folder_locks_id">

</Samples>

<Message type="notice">

# フォルダのロックIDを見つける方法

フォルダのロックを削除するには、フォルダのロックIDをAPIに指定する必要があります。フォルダのロックIDは、[フォルダのロックを作成](g://folders/single/create-lock/)したとき、または特定のフォルダに対する[ロックのリストを取得](g://folders/single/get-locks/)したときに、応答に示されます。

</Message>
