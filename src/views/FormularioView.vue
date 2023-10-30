<template>
    <div>
        <formulario :user="user"  />
    </div>
</template>

<script setup lang="ts">
  import { onBeforeMount, ref } from "vue";
  import formulario from '@/components/Formulario.vue';
  import { useRoute } from 'vue-router';
  import { API } from "@/constantes";
  import type { ITarea } from "@/constantes";

  const { params } = useRoute()
  const user = ref<null | ITarea>(null)
  // console.log(params)

  onBeforeMount(async () => {
    if(params.id) {
      const data = await fetch(`${API}/?id=${params.id}`)
      
      user.value =  await data.json()
      console.log(user.value)
    }
    
  })

</script>

<style scoped>

</style>