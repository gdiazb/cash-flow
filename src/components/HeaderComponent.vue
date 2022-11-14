<template>
  <header class="header">
    <img
      src="@/assets/img/cashflow-icon.svg"
      alt=""
      class="header__logo"
      @click="reload"
    />
    <h1 class="header__title">Cash<span>Flow</span></h1>
  </header>
</template>

<script>
export default {
  methods: {
    reload() {
      location.reload();
    },
  },
};
</script>

<style scoped>
@import "@/assets/styles/components/header.scss";
</style>
