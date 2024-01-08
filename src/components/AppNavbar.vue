<template>
  <nav>
    <el-icon  @click="$emit('logo-clicked')" class="logo" ><Expand style="width: 75%;height: 75%;"/></el-icon>
    <router-link class="router-link" to="/"> 主页 </router-link>
    <router-link class="router-link" to="/doing"> 在做什么呢 </router-link>
    <router-link class="router-link" to="/blogs"> 博客 </router-link>
    <el-button style="margin-left:auto;background-color:#02bd7e;border-color: #02bd7e;color: black; "
      @click="toggleTheme" round><el-icon><Opportunity /></el-icon></el-button>
  </nav>
</template>

<script setup lang="ts">
import { ref, onMounted } from "vue";
import router from "@/router";
function GetCookie(name: string) {
  const cookies = document.cookie.split(';');
  for (let i = 0; i < cookies.length; i++) {
    const cookie = cookies[i].trim();
    if (cookie.startsWith(name + '=')) {
      return cookie.substring(name.length + 1);
    }
  }
  return '';
}
const toggleTheme = () => {
  // 从 cookie 中获取当前主题
  const currentTheme = GetCookie('theme');
  if (currentTheme === 'dark') {
    // 如果当前主题是 dark，那么切换到 light 主题
    document.documentElement.classList.remove('dark-theme');
    document.documentElement.classList.add('light-theme');

    // 更新 cookie
    document.cookie = 'theme=light; path=/';
  } else {
    // 如果当前主题是 light 或者没有设置主题，那么切换到 dark 主题
    document.documentElement.classList.remove('light-theme');
    document.documentElement.classList.add('dark-theme');

    // 更新 cookie
    document.cookie = 'theme=dark; path=/';
  }
}
</script>

<!-- Your styles here -->
<style scoped>

.dark-theme nav{
  background-color: #141414;
}


.light-theme nav{
  background-color:#ffffff;
}

nav {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  display: flex;
  align-items: center;
  /* 垂直居中 */
  height: 70px;
  font-size: 1rem;
  /* 其他样式属性 */

  /* 添加一些边框和阴影 */
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
}

/* 调整链接的样式 */
.router-link {
  text-decoration: none;
  padding: 10px;
  /* 调整链接内部的内边距 */
  border-radius: 5px;
  /* 圆角 */
  transition: background-color 0.3s ease;
  /* 添加过渡效果 */
}
.router-link:hover {
  scale: 1.15;
}
.router-link-right {
  text-decoration: none;
  padding: 10px;
  /* 调整链接内部的内边距 */
  border-radius: 100px;
  /* 圆角 */
}

.router-link-right:hover {
  text-decoration: none;
  padding: 10px;
  /* 调整链接内部的内边距 */
  border-radius: 100px;
  /* 圆角 */
  pointer-events: none;

}

.logo {
  width: 40px;
  height: 40px;
  margin-left: 15px;
  margin-right: 5px;
  color: rgb(68, 194, 76);

}
.logo:hover {
  scale: 1.15;
}
.el-button {
  transition: transform 0.3s ease;
}

.el-button:hover {
  transform: scale(1.1);
}

@keyframes click {
  0% {
    transform: scale(1.1);
  }

  50% {
    transform: scale(0.9);
  }

  100% {
    transform: scale(1);
  }
}

.el-button:active {
  animation: click 0.5s;
}</style>
<style>

.dark-theme .el-popper{
  background-color: #252525!important;
  border-width: 0!important;
}
.dark-theme .el-dropdown-menu{
  background-color: #252525!important;
  color: white!important;
}
.dark-theme .el-dropdown-menu__item{
  color: white!important;
}
.dark-theme .el-dropdown-menu__item:hover{
  background-color: #151515!important;
  color: white!important;
}

.light-theme .el-popper{
  background-color: #ffffff!important;
  border-width: 0!important;
}
.light-theme .el-dropdown-menu{
  background-color: white!important;
  color: #252525!important;
}
.light-theme .el-dropdown-menu__item{
  color: #252525!important;
}
.light-theme .el-dropdown-menu__item:hover{
  background-color: #dddddd!important;
  color: #151515!important;
}

</style>