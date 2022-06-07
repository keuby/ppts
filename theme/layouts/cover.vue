<template>
  <div
    class="slidev-layout cover bg-no-repeat bg-cover bg-left bg-top cover-bg bg-white text-white"
  >
    <div class="my-auto w-full">
      <slot></slot>
    </div>
    <img class="absolute top-7 left-7 w-60" src="../images/logo.png" />
  </div>
</template>

<style scoped>
.cover-bg {
  background: url("../images/background.png");
}
</style>
