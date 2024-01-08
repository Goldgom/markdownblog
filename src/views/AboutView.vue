<template>
  <div class="about">
    <h1>This is an about page</h1>
  </div>
</template>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
.light-theme .card-text {
  color: black;
}
.dark-theme .card-text {
  color: white;
}

.light-theme .title {
  color: black;
}
.dark-theme .title,h1,h2,h3 {
  color: white;
}
</style>
