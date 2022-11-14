<template>
  <div>
    <h2 class="movements__title">Historial</h2>
    <ul class="movements__list">
      <Movement
        v-for="{ id, title, description, amount } in movements"
        :key="id"
        :id="id"
        :title="title"
        :description="description"
        :amount="amount"
        @remove="remove"
      >
      </Movement>
    </ul>
  </div>
</template>

<script setup>
import { defineProps, toRefs, defineEmits } from "vue";
import Movement from "@/components/Movements/Movement.vue";
const props = defineProps({
  movements: {
    type: Array,
    default: () => [],
  },
});
const { movements } = toRefs(props);
const emit = defineEmits(["remove"]);

const remove = (id) => {
  emit("remove", id);
};
</script>

<style scoped lang="scss">
@import "@/assets/styles/components/movements.scss";
</style>
