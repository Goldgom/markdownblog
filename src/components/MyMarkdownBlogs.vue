<template>
    <main>
        <el-card class="box-card">

            <div v-html="renderedMarkdown"></div>
        </el-card>
    </main>
</template>

<script lang="ts" setup>
import MarkdownIt from 'markdown-it';
import markdownItMathjax from 'markdown-it-mathjax3';
import { useRouter } from 'vue-router';

import markdownItHighlightjs from 'markdown-it-highlightjs';
import 'highlight.js/styles/tomorrow-night-bright.css';
import axios from 'axios';
import { jsonp } from 'vue-jsonp'

import { ref, onMounted, computed } from 'vue';
const props = defineProps({
    git: String,
    path: {
        type: Array as () => Array<string>,
        default: () => [],
    },
});

const md = new MarkdownIt();
const markdown = ref('');
md.use(markdownItHighlightjs);
const git = ref(props.git || '');
const path = ref(props.path && Array.isArray(props.path) ? props.path.join('/') : 'README.md');
md.use(markdownItMathjax, {
  tex: {
    inlineMath: [['$', '$'], ['\\(', '\\)']], // 内联数学公式
    displayMath: [['$$', '$$'], ['\\[', '\\]']], // 显示数学公式
    processEscapes: true, // 允许在数学公式中使用反斜杠进行转义
    processEnvironments: true, // 允许使用 LaTeX 环境
  }
});
const router = useRouter();

const navigateTo = (url: string) => {
  const currentPath = router.currentRoute.value.fullPath;
  const newPath = currentPath.endsWith('/') ? currentPath + url : `${currentPath}/${url}`;
  router.push(newPath);
};
const defaultRender = md.renderer.rules.link_open || function(tokens: any[], idx: number, options: any) {
  return md.renderer.renderToken(tokens, idx, options);
};

md.renderer.rules.link_open = function (tokens: any[], idx: number, options: any) {
  // 找到 href 属性的索引
  const hrefIndex = tokens[idx].attrIndex('href');
  if (hrefIndex >= 0) {
    // 如果找到了 href 属性，获取它的值
    const hrefValue = tokens[idx].attrs[hrefIndex][1];
    // 获取当前路径
    const currentPath = window.location.pathname;
    // 确保 currentPath 不是以 / 结尾
    const normalizedCurrentPath = currentPath.endsWith('/') ? currentPath.slice(0, -1) : currentPath;
    // 确保 hrefValue 不是以 / 开头
    const normalizedHrefValue = hrefValue.startsWith('/') ? hrefValue.slice(1) : hrefValue;
    // 将当前路径、/ 和 href 值拼接起来
    tokens[idx].attrs[hrefIndex][1] = normalizedCurrentPath + '/' + normalizedHrefValue;
  } else {
    // 如果没有找到 href 属性，添加它
    tokens[idx].attrPush(['href', 'javascript:void(0)']);
  }
  return defaultRender(tokens, idx, options);
};
const renderedMarkdown = ref('');
onMounted(async () => {
    try {
        console.log(git.value + path.value);
        const response = await fetch(git.value + path.value);
        const text = await response.text();
        markdown.value = text;
        console.log(markdown.value);
        renderedMarkdown.value = md.render(markdown.value);
    } catch (error) {
        console.error("HTTP error " + error);
    }
});
</script>

<style scoped>
main{
    overflow-y: auto;
}
.box-card {
    width: 80%;
    min-height: 50%;
    margin-left: 10%;
    margin-top: 20px;
    border-radius: 30px;
    border-width: 0;
    box-shadow: 1px 2px 4px rgba(0, 0, 0, 0.2);

}
.box-card:hover {
    scale: 1.01;
    }
.dark-theme .box-card {
    background-color: #101010;
    color: white;
}
.light-theme .box-card {
    background-color: #ffffff;
    color: black;
}
</style>
