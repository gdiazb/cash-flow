<template>
  <main class="resume__main">
    <p>{{ labelVisual }}</p>
    <h1>{{ amountCurrency }}</h1>
    <div class="graphic">
      <slot name="graphic"></slot>
    </div>
    <div class="action">
      <slot name="action"></slot>
    </div>
  </main>
</template>

<script>
import currencyFormater from "@/functions/currencyFormater";

export default {
  props: {
    label: {
      default: null,
      type: String,
    },
    totalLabel: String,
    amount: {
      default: null,
      type: Number,
    },
    totalAmount: Number,
  },
  computed: {
    labelVisual() {
      return this.label !== null ? this.label : this.totalLabel;
    },
    amountVisual() {
      return this.amount !== null ? this.amount : this.totalAmount;
    },
    amountCurrency() {
      return currencyFormater.format(this.amountVisual);
    },
  },
};
</script>

<style scoped lang="scss">
@import "@/assets/styles/components/resume.scss";
</style>
