<template>
  <div class="slidev-layout default bg">
    <div class="my-auto flex flex-col h-full">
      <img src="../images/logo-dark.png" class="h-10 absolute top-5.2 right-3" />
      <div class="flex-1 overflow-hidden">
        <slot></slot>
      </div>
      <div class="flex justify-end">
        <img class="w-60 -mr-12" src="../images/footer.png" />
      </div>
    </div>
  </div>
</template>
