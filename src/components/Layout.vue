<template>
  <div class="wrapper">
    <slot name="header"></slot>
    <slot name="resume"></slot>
    <div class="movements">
      <div class="movements__head" @click="showMovements = !showMovements">
        <span class="movements__grip"></span>
      </div>
      <div class="movements__main" :class="{ disabled: !showMovements }">
        <slot name="movements"></slot>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const showMovements = ref(false);
</script>

<style scoped lang="scss">
@import "@/assets/styles/components/layout";
</style>
