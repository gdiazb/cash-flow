<template>
  <Layout>
    <template #header>
      <HeaderComponent></HeaderComponent>
    </template>
    <template #resume>
      <Resume
        :total-label="'Ahorro total'"
        :label="label"
        :total-amount="totalAmount"
        :amount="amount"
      >
        <template #graphic>
          <Graphic :amounts="amounts" @select="select" />
        </template>
        <template #action>
          <Action @create="create"></Action>
        </template>
      </Resume>
    </template>
    <template #movements>
      <Movements :movements="movementsList" @remove="remove"></Movements>
    </template>
  </Layout>
</template>

<script>
import Layout from "@/components/Layout";
import HeaderComponent from "@/components/HeaderComponent";
import Resume from "@/components/Resume/";
import Graphic from "@/components/Resume/Graphic";
import Movements from "@/components/Movements";
import Action from "@/components/Action";

export default {
  components: {
    Layout,
    HeaderComponent,
    Resume,
    Movements,
    Action,
    Graphic,
  },
  data() {
    return {
      amount: null,
      label: null,
      movementsList: [],
    };
  },
  computed: {
    amounts() {
      const lastDays = this.movementsList
        .filter((m) => {
          const today = new Date();
          const oldDate = today.setDate(today.getDate() - 30);
          return m.time > oldDate;
        })
        .map((m) => m.amount);

      return lastDays.map((m, i) => {
        const lastMovements = lastDays.slice(0, i + 1);
        return lastMovements.reduce((suma, movement) => {
          return suma + movement;
        }, 0);
      });
    },
    totalAmount() {
      return this.movementsList.reduce((suma, m) => {
        return suma + m.amount;
      }, 0);
    },
  },
  mounted() {
    const movementsList = JSON.parse(localStorage.getItem("movementsList"));
    if (Array.isArray(movementsList)) {
      this.movementsList = movementsList.map((m) => {
        return { ...m, time: new Date(m.time) };
      });
    }
  },
  methods: {
    create(movement) {
      this.movementsList.push(movement);
      this.save();
    },
    remove(id) {
      const index = this.movementsList.findIndex((m) => m.id === id);
      this.movementsList.splice(index, 1);
      this.save();
    },
    save() {
      localStorage.setItem("movementsList", JSON.stringify(this.movementsList));
    },
    select(el) {
      this.amount = el;
    },
  },
};
</script>
