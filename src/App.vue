<template>
  <AppNavbar class="nav-view" />
  <RouterView class="main-view" />
</template>

<script setup lang="ts">

import 'element-plus/dist/index.css'
import AppNavbar from './components/AppNavbar.vue';
import { onMounted } from 'vue';

import { RouterLink, RouterView } from 'vue-router'
function setChatStyleFromCookieOrDefault() {
  // 从 cookie 中读取 chatStyle
  let chatStyle = document.cookie.split('; ').find(row => row.startsWith('chatStyle='))?.split('=')[1];

  document.documentElement.classList.remove('bubble-message-style');
  document.documentElement.classList.remove('chatroom-message-style');

  if (!chatStyle) {
    // 如果 cookie 中没有 chatStyle，就设置默认的聊天样式
    chatStyle = 'chatroom-message-style';

    // 将默认的聊天样式保存到 cookie
    document.cookie = `chatStyle=${chatStyle}; path=/`;
  }

  // 使用 chatStyle 设置聊天样式
  document.documentElement.classList.add(chatStyle);
}
function setThemeFromCookieOrSystem() {
  // 从 cookie 中读取 theme
  let theme = document.cookie.split('; ').find(row => row.startsWith('theme='))?.split('=')[1];

  document.documentElement.classList.remove('dark-theme');
  document.documentElement.classList.remove('light-theme');

  if (!theme) {
    // 如果 cookie 中没有 theme，就检查系统的颜色方案
    if (window.matchMedia('(prefers-color-scheme: dark)').matches) {
      theme = 'dark';
    } else {
      theme = 'light';
    }
    // 将系统的颜色方案保存到 cookie
    document.cookie = `theme=${theme}; path=/`;
  }

  // 使用 theme 设置主题
  document.documentElement.classList.add(theme+'-theme');
}
onMounted(() => {
  setThemeFromCookieOrSystem();
  setChatStyleFromCookieOrDefault();
const font = document.createElement('link');
font.href = 'https://fonts.googleapis.com/css2?family=Noto+Sans+SC&display=swap';
font.rel = 'stylesheet';
font.crossOrigin = 'anonymous';
document.body.appendChild(font);
});
</script>



<style>

p {
    font-family: 'Noto Sans SC', sans-serif;
}
a{
    font-family: 'Noto Sans SC', sans-serif;
}

.dark-theme a{
  color: rgb(68, 194, 76);
}
.dark-theme body{
  background-color: #151515;
}

.light-theme body{
  background-color: #f5f5f5;
}
.light-theme a{
  color: rgb(68, 194, 76);
}

a:hover {
  /* Reset the styles to the non-hover state */
  background-color: transparent;
}
.nav-view {
  position: fixed;
  width: 100%;
  height: 70px;
  z-index: 1000;

}

.main-view {
  position: fixed;
  width: 100%;
  height: calc(100% - 70px);
  left: 0;
  top: 70px;
}
</style>

