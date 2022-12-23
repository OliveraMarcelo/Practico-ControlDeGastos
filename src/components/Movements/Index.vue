<template>
    <div class="movements">
        <h2 class="title">Historial</h2>
        <div class="content">
          <Movement v-for="{id,title,description,amount} in movements" 
          :key="id" 
          :id="id" 
          :title="title"
          :description="description"
          :amount="amount"
          @remove="remove"
          >
          </Movement>
        </div>
    </div>
</template>

<script setup>
import Movement from "./Movement.vue"
import { defineProps,toRefs,defineEmits } from 'vue';
const props = defineProps({
  movements : {
    type : Array,
    default: ()=>[],
  }
})

const remove = (id)=>{
emit("remove",id)
}

const {movements} = toRefs(props)

const emit = defineEmits(["remove"])
</script>

<style scoped>
.movements {
  max-height: 100%;
  padding: 0 8px;
  margin-bottom: 14px;
}

.title {
  margin: 8px 16px 24px 16px;
  color: rgb(15, 186, 253);
}

.content {
  max-height: 68vh;
  display: flex;
  flex-direction: column;
  gap: 8px;
  overflow-y: scroll;
}
</style>