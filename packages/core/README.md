# 自定义 `markdownItDataBlock` 插件

> 如果你在做AI相关的工作，可能会用到这个插件。它可以帮助你在markdown中嵌入数据块，并且支持自定义标签和数据格式。

## 1. 使用方法

> _注意是类 fence 语法，最好输出是使用换行符包裹避免出现意外情况_

- 直接在 `markdown` 中使用 `yugu` 标签，标签的开始和结束都需要添加 `yugu-start` 和 `yugu-end`，中间可以放置任意内容。
- 支持自定义开始结束标签对应的`tag`, 例如`app`，`sub`，`yugu-start` 和 `yugu-end` 中的 `tag` 属性值需要一致。必须使用`[]`包裹
- 支持自定义数据，数据可以是字符串和 json 对象，json 对象需要转义。且数据必须用`$`包裹
- 支持嵌套标签，嵌套标签必须成对，不能跨`yugu-xx`分开。

## 2. 依赖

插件依赖`markdown-it-attrs`，需要在 `markdown-it` 中注册该插件。

## 3. 示例

```js
import MarkdownIt from 'markdown-it'
import markdownItAttrs from 'markdown-it-attrs'
import markdownItDataBlock from '@yuguaa/markdown-it-data-block'
const md = new MarkdownIt()
  .use(markdownItAttrs)
  .use(markdownItDataBlock)
const html = md.render(
  `::: yugu-start[app]\${"a": 1,"b":[{"c":222}]}\$
    app 块内容
    \n::: yugu-start[sub]\${"a": 1,"b":[{"c":55}]}\$
    sub 块内容
    \n::: yugu-end[sub]\$支持嵌套，但必须合并标签嵌套\$
    app 块内容结束，在app块内
    \n::: yugu-end[app]\$这里是数据，可以是字符串和json\$
    app 块内容外`
)
console.log(html)

```

```javascript
// 注意流式情况下包裹换行符号避免意外情况
'::: yugu-start[app]${"a":1,"b":[{"c":222}]}$ \napp开始了\n # 一级标题\n::: yugu-start[sub]\n # 二级标签开始了\n::: yugu-end[sub]\n- [ ] 7:30-8:00 晨跑3公里\n- [ ] 每工作1小时起身拉伸/喝水\n\n\n # 二级标签结束了\n \n\n::: yugu-end[app]$这里是数据，可以是字符串和json$\n'
```
