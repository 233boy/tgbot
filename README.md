# tgbot

[233blog TG 群组](https://t.me/blog233) 自动回复机器人的处理规则 

## Match 规则

match 是一个数组，里面存放所有处理规则。请参考：[match.json](match.json)

```json
{
    "match": [
        {
            "name": "hello world",
            "type": "reply",
            "regex": [
                "hello",
                "!!!test",
                "world"
            ],
            "content": "发现 hello world 啦！！！",
            "replyToMsg": false
        }
    ]
}
```

> `name`: "string"

可选。用来备注一个规则

> `type`: "reply" | "delete"

必填。规则的类型，可选 "reply" 或 "delete"
- reply
    - 回复一条消息
- detele
    - 删除一条消息


> `regex`: [ string ]

必填。一个正则数组，用于匹配消息

你可以使用 `!!!` 来排除关键词，`!!!` 选项亦同时正则。

当一条消息完全匹配此正则数组的时候，响应此规则。

备注1：不分区大小写，并且全局匹配。

备注2：假设你要使用 `\d` 匹配一个数字，请写成 `\\d`。否则 JSON 会报错

小提示：为提高匹配性能，请将要匹配的主要关键词放到首位，然后排除关键词放到第二位，接着放其他关键词。

> `content`: "string"

必填。用于回复消息时的内容，当 `type` 为 "delete" 时可留空。

备注：支持 Markdown 语法，如需换行请使用 `\n`

> `replyToMsg`: false | true

必填。是否将消息回复到匹配到的消息，可选 false 或 true

当 `replyToMsg` 为 true 时将消息回复到匹配到的消息，否则以新消息形式发送。

备注：当 `type` 为 "delete" 时此选项不生效。

## 例子

匹配讨论 Cloudflare 速度慢的消息。

```json
{
    "type": "reply",
    "regex": [
        "cf|cloud\\s*flare",
        "慢",
        "中转|速度"
    ],
    "content": "慢是正常，快是意外。",
    "replyToMsg": true
}
```
