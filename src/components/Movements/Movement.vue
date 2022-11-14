<template>
  <div class="movement">
    <div class="movement__content">
      <h4>{{ title }}</h4>
      <p>{{ description }}</p>
    </div>
    <div class="movement__values">
      <img src="@/assets/img/trash-icon.svg" alt="eliminar" @click="remove" />
      <p
        :class="{
          red: isNegative,
          green: !isNegative,
        }"
      >
        {{ amountCurrency }}
      </p>
    </div>
  </div>
</template>

<script setup>
import { toRefs, defineProps, defineEmits, computed } from "vue";
import currencyFormater from "@/functions/currencyFormater";

const props = defineProps({
  id: {
    type: Number,
  },
  title: {
    type: String,
  },
  description: {
    type: String,
  },
  amount: {
    type: Number,
  },
});
const { id, title, description, amount } = toRefs(props);

const amountCurrency = computed(() => currencyFormater.format(amount.value));
const isNegative = computed(() => amount.value < 0);

const emit = defineEmits(["remove"]);

const remove = () => {
  emit("remove", id.value);
};
</script>

<style scoped>
@import "@/assets/styles/components/movement.scss";
</style>
