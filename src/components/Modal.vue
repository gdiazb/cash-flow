<template>
  <div class="modal">
    <header class="modal__head">
      <p class="modal__text">Nuevo movimiento</p>
      <img src="@/assets/img/close-icon.svg" alt="cerrar" @click="close" />
    </header>
    <div class="modal__body">
      <slot></slot>
    </div>
  </div>
</template>

<script setup>
import { defineEmits } from "vue";

const emit = defineEmits(["close"]);
const close = () => emit("close");
</script>

<style lang="scss" scoped>
@import "@/assets/styles/components/modal.scss";
</style>
