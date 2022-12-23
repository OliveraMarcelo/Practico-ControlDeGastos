<template>
  <main>
    <p>{{ labelVisual }}</p>
    <h1 :class="{
      'red': isNegative,
      'green': !isNegative
    }">{{ amountCurrency }}</h1>
    <div class="graphic">
      <slot name="graphic"></slot>
    </div>
    <div class="action">
      <slot name="action"></slot>
    </div>
  </main>
</template>

<script setup>
import { computed } from 'vue';
const currencyFormatter = new Intl.NumberFormat("es-AR", {
  style: "currency",
  currency: "ARS",
})
const props = defineProps({
  amount: Number,
  label: String,
  totalAmount: Number,
  totalLabel: String,
})
let amountVisual = computed(() => props.amount !== null ? props.amount : props.totalAmount)
const labelVisual = computed(() => props.label !== undefined ? props.label : props.totalLabel)
const amountCurrency = computed(() => currencyFormatter.format(amountVisual.value))
const isNegative = computed(()=> amountVisual.value < 0 )

console.log(amountVisual.value);

</script>

<style scoped>
* {
  font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif
}

main {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  width: 100%;
}

h1,
p {
  margin: 0;
  text-align: center;
}

h1 {
  margin-top: 14px;
  color: green;
}

.graphic {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  padding: 48px 24px;
  box-sizing: border-box;
}
.red {
    color: red;
}
.green {
    color: green;
}
</style>