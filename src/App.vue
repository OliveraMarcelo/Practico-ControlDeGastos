<template>

<Suspense>
  <template #default>
    <Home/>
  </template>

  <template #fallback>
    <Welcome/>
  </template>
</Suspense>

</template>

<script>
//Utilizando defineAsyncComponent para mostrar un tiempo de forma asincrona
// y utilizando slots 
//import Home from "@/components/Home.vue"
import Welcome from "@/components/Welcome.vue"
import { defineAsyncComponent } from "vue";
export default {
  name: "App",
  components:{
    Welcome,
    Home:defineAsyncComponent(() => 
      new Promise((resolve) => {
        setTimeout(() => {
          resolve(import("./components/Home.vue"))
        },2500);
      })
     ),
  }
};
</script>

<style>
*{
  margin: 0;
  padding: 0;
  font-family:'Courier New', Courier, monospace;
}
</style>
