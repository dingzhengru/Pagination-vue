# Pagination-vue
因其他專案需要而寫的分頁物件，使用 vue 寫的 Component  
雖然原專案 css 是套 Bootstrap，但此專案主要是紀錄 JS 邏輯


## 注意
* 主要差別是: 給 Array 而不是 Page Count

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

