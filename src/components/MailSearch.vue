<script setup></script>
<template>
  <div class="w-full flex flex-col">
    <div class="flex">
      <slot></slot>
    </div>

    <div class="w-full flex justify-center">
      <slot name="header"></slot>
    </div>
  </div>
</template>
<style scoped></style>
