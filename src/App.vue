<template>
  <div>
    <Suspense>
      <template #default>
        <Home></Home>
      </template>
      <template #fallback>
        <SplashScreen></SplashScreen>
      </template>
    </Suspense>
  </div>
</template>

<script>
import SplashScreen from "@/components/SplashScreen.vue";
import { defineAsyncComponent } from "vue";

export default {
  components: {
    SplashScreen,
    Home: defineAsyncComponent(() => {
      return new Promise((resolve) => {
        setTimeout(() => {
          resolve(import("./components/HomePage.vue"));
        }, 2500);
      });
    }),
  },
};
</script>

<style lang="scss">
@import "@/assets/styles/components/app-page.scss";
</style>
