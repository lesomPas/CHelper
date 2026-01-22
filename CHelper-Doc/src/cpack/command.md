# 命令的注册

在个根目录中，有一个`command`的文件夹用于存储命令，里面的每个 json 文件对应一个命令。

```json
{
  "name": ["ability"],
  "description": "赋予或剥夺玩家的能力",
  "start": ["player"],
  "node": [
    {
      "type": "TARGET_SELECTOR",
      "id": "player",
      "description": "要赋予或剥夺能力的玩家",
      "isOnlyOne": false,
      "isMustPlayer": true,
      "isMustNPC": false
    },
    {
      "type": "NORMAL_ID",
      "id": "ability",
      "description": "要操作的能力",
      "ignoreError": false,
      "contents": [
        {
          "name": "worldbuilder",
          "description": "给予玩家成为世界建造者的能力"
        },
        {
          "name": "mayfly",
          "description": "给予飞行的能力"
        },
        {
          "name": "mute",
          "description": "将玩家禁言，聊天时其他人将无法看见或听见目标"
        }
      ]
    },
    {
      "type": "BOOLEAN",
      "id": "value",
      "description": "此能力是否对玩家可用",
      "descriptionTrue": "此能力对玩家可用",
      "descriptionFalse": "此能力对玩家不可用"
    }
  ],
  "ast": [
    ["player", "ability", "LF"],
    ["ability", "value"],
    ["value", "LF"]
  ]
}
```

|    名字     |    类型    |      含义      |                                   备注                                   | 必需 |
| :---------: | :--------: | :------------: | :----------------------------------------------------------------------: | :--: |
|    name     | 字符串列表 |   命令的名字   |                                    -                                     |  是  |
| description |   字符串   |   命令的介绍   |                                    -                                     |  否  |
|    node     |  节点列表  |    节点列表    |                             列举所有命令参数                             |  是  |
|    start    | 字符串列表 | 命令的起始节点 |                     由于节点类型太多，会在后面单独讲                     |  是  |
|     ast     |  关系列表  |    关系绑定    | 存储着多个数组，其中的每个数组第一个 ID 代表父节点，后面的元素当作子节点 |  否  |

::: tip
在 node 节点列表中，每个节点有个 ID，在加载好节点列表后，程序再根据后面的 start 和 ast 用这个 ID 来绑定节点的位置。
:::
