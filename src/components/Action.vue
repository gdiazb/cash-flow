<template>
  <div>
    <button class="action__button" @click="showModal = true">
      Agregar movimiento
    </button>
    <teleport to="#app">
      <Modal v-show="showModal" @close="showModal = false">
        <form @submit.prevent="submit">
          <div class="field">
            <label>Título</label>
            <input type="text" v-model="title" />
          </div>
          <div class="field">
            <label>Monto</label>
            <input type="number" v-model="amount" />
          </div>
          <div class="field">
            <label>Descripción</label>
            <textarea rows="4" v-model="description"></textarea>
          </div>
          <div class="field">
            <label class="radio-label">
              <input type="radio" v-model="movementType" value="Ingreso" />
              <span>Ingreso</span>
            </label>
            <label class="radio-label">
              <input type="radio" v-model="movementType" value="Gasto" />
              <span>Gasto</span>
            </label>
          </div>
          <div class="action">
            <button class="action__button">Agregar movimiento</button>
          </div>
        </form>
      </Modal>
    </teleport>
  </div>
</template>

<script setup>
import { ref, defineEmits } from "vue";
import Modal from "./Modal.vue";

const showModal = ref(false);

const title = ref("");
const amount = ref(0);
const description = ref("");
const movementType = ref("Ingreso");

const emit = defineEmits(["create"]);

const refreshForm = () => {
  title.value = "";
  amount.value = 0;
  description.value = "";
  movementType.value = "Ingreso";
};

const submit = () => {
  showModal.value = false;
  emit("create", {
    title: title.value,
    description: description.value,
    amount: movementType.value === "Ingreso" ? amount.value : -amount.value,
    time: new Date(),
    id: new Date().getTime(),
  });
  refreshForm();
};
</script>

<style scoped lang="scss">
@import "@/assets/styles/components/action.scss";
</style>
