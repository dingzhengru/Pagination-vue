# Pagination-vue
因專案需要而寫的分頁物件，使用 vue 寫的 Component

## 給 Array 而不是 Page Count
* 主要差別是，

## Props
| 屬性名     | 型態    | 說明              | 預設  |
|-----------  |-------- |------------------ |------ |
| data        | Array   | 資料              | []    |
| startpage   | Number  | 初始頁碼          | 1     |
| pagesize    | Number  | 一頁顯示多少資料  | 10    |
| pagerange   | Number  | 顯示多少頁碼      | 3     |

## Events
| 事件名       | 回傳型態  | 觸發          | 說明          |
|-------------  |---------- |-------------  |-------------- |
| page-data     | Array     | data 改變時  | 回傳該頁資料  |
| change-page   | Number    | page 改變時  | 回傳目前頁碼  |

