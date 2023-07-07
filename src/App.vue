<template>
  <div class="main">
    <RouterView />
  </div>
</template>

<style scoped>
body {
  direction: rtl !important;
  text-align: right !important;
}
.main {
  margin: 0 auto;
  min-width: 500px;
}
</style>
