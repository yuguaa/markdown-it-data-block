<script setup>
import MarkdownIt from 'markdown-it'
import MarkdownItAttrs from 'markdown-it-attrs'
import MarkdownItDataBlock from '@yugu/markdown-it-data-block'
const md = new MarkdownIt().use(MarkdownItAttrs).use(MarkdownItDataBlock)
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
</script>

<template>
  <div v-html="html"></div>
</template>

<style scoped></style>
