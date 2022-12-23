<template>
  <Layout>
    <template #header>
      <Header />
    </template>
    <template #resume>
      <Resume :label="'Ahorro total'" :totalLabel="'Ahorro del mes'" :totalAmount="totalAmount" :amount="amount">
        <template #graphic>
          <Graphic :amounts="amounts" @select="select" />
        </template>
        <template #action>
          <Action @create="create" />
        </template>
      </Resume>
    </template>
    <template #movements>
      <Movements :movements="movements" @remove="remove" />
    </template>
  </Layout>
</template>

<script setup>
import { ref, computed, reactive, onBeforeMount } from 'vue'
import Action from "../components/Action.vue"
import Header from "../components/Header.vue";
import Layout from "../components/Layout.vue";
import Resume from "../components/Resume/Resume.vue";
import Graphic from "../components/Resume/Graphic.vue";
import Movements from "./Movements/Index.vue";

const movements = ref([])

const amount = ref(null)

onBeforeMount(() => {
  const movementsLS = JSON.parse(localStorage.getItem("movements"))
  if (Array.isArray(movementsLS)) {
    movements.value = movementsLS.map(m => {
      return { ...m, time: new Date(m.time) }
    })
  }
})

const amounts = computed(() => {
  const lastDays = movements.value
    .filter((movement) => {
      console.log(movement);
      const today = new Date()
      const oldDate = today.setDate(today.getDate() - 30)
      return movement.time > oldDate;
    }).map(movement => movement.amount);
  return lastDays.map((m, i) => {
    const lastMovements = lastDays.slice(0, i + 1);
    console.log(lastMovements);
    return lastMovements.reduce((suma, movement) => {
      return suma + movement
    }, 0);
  });
})

const totalAmount = computed(() => {
  console.log(movements.value)
  return movements.value.reduce((suma, m) => {
    console.log(suma, m.amount);
    return suma + m.amount;
  }, 0)
})

const create = (movement) => {
  movements.value.push(movement)
  save()
}
const remove = (id) => {
  const index = movements.value.findIndex(m => m.id === id)
  movements.value.splice(index, 1)
  save()
}
const save = () => {
  localStorage.setItem("movements", JSON.stringify(movements.value))
}

const select = (el) => {
  console.log(el);
  amount.value = el
}

</script>

<style scoped>
.splashscreen {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  height: 100vh;
}
</style>