<script setup lang="ts">
import TheWelcome from '../components/TheWelcome.vue'
import HelloWorld from '../components/HelloWorld.vue'

</script>

<template>
  <header>
    <HelloWorld msg="Hi，这里是Goldgom" />
  </header>
  <main>
    <TheWelcome />
  </main>
  <footer>
<a href="https://beian.miit.gov.cn/" target="_blank">苏ICP备2023032616号-1</a>  </footer>
</template>
<style>
header {
  line-height: 1.5;
  margin-top: 2rem;
  max-height: 100vh;
  font-family: 'Noto Sans SC', sans-serif;
}
footer {
  position:fixed;
  left: 0;
  bottom: 0;
  width: 100%;
  text-align: center;
  background-color: white;
  padding: 0.5rem 0;
  font-family: 'Noto Sans SC', sans-serif;
}
.dark-theme  footer{
  background-color: #181818;
}
footer p {
  margin: 0;
  color: #6c757d;
  font-size: 0.875rem;
}

@media (min-width: 1024px) {
  header {
    margin-top: 2rem;
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }


}
</style>