<script setup lang="ts">
import WelcomeItem from './WelcomeItem.vue'
import DocumentationIcon from './icons/IconDocumentation.vue'
import ToolingIcon from './icons/IconTooling.vue'
import EcosystemIcon from './icons/IconEcosystem.vue'
import CommunityIcon from './icons/IconCommunity.vue'
import SupportIcon from './icons/IconSupport.vue'
</script>

<template>
  <WelcomeItem>
    <template #icon>
      <DocumentationIcon />
    </template>
    <template #heading>我的碎碎念</template>

    我的碎碎念会记录在这里
    
  </WelcomeItem>

  <WelcomeItem>
    <template #icon>
      <ToolingIcon />
    </template>
    <template #heading>我的作品</template>
      我会有好多好多作品罢，快端出来吧~
    <br />

  </WelcomeItem>

  <WelcomeItem>
    <template #icon>
      <EcosystemIcon />
    </template>
    <template #heading>bilibili</template>
      这里是我的bilibili主页，欢迎来玩~

  </WelcomeItem>

  <WelcomeItem>
    <template #icon>
      <CommunityIcon />
    </template>
    <template #heading>github</template>
      嗯，一个合格的程序员怎么能没有github呢？

  </WelcomeItem>

  <WelcomeItem>
    <template #icon>
      <SupportIcon />
    </template>
    <template #heading>给点赞助罢~</template>
      如果你觉得我的作品还不错，可以考虑给我点赞助，这样我就可以更有动力做出更多好玩的东西啦~
  </WelcomeItem>
</template>

<style scoped>
.dark-theme .icon-style {
    fill: white;
  /* 在这里添加你的样式 */
}
.light-theme .WelcomeItem::heading {
  color: white;
  background-color: #151515;
  border: 1px solid #151515;
}

:root{
  font-family: 'Noto Sans SC', sans-serif;
}
</style>
