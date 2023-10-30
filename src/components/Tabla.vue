<template>
    <div>
        <h1>Usuarios</h1>
        <table class="table table-success table-striped-columns">
          <thead>
          <tr>
            <th >ID</th>
            <th >Name</th>
            <th >LastName</th>
            <th>Mail</th>
            <th>Editar</th>
            <th>Eliminar</th>
          </tr>
        </thead>
        <tbody class="table-group-divider">
          <tr v-for="usuario in usuarios" :key="usuario.id">
            <th>{{ usuario.id }}</th>
            <th>{{ usuario.name }}</th>
            <th>{{ usuario.lastname }}</th>
            <th>{{ usuario.email }}</th>
            <th @click="editar(usuario.id)">👁️</th>
            <th @click="eliminar(usuario)">🗑️</th>
          </tr>
        </tbody>
        </table>

    </div>
</template>

<script setup lang="ts">
import { onMounted, ref } from "vue";
import { API } from "@/constantes";
import type { ITarea } from "@/constantes";
import { useRouter } from 'vue-router';

const usuarios = ref<ITarea[]>([]);
  const router = useRouter();

const editar = (id:number) => {
  router.push(`/tareas-formulario/${id}`)
} 

const eliminar = async ({id, name, lastname}:ITarea) => {
 const res =  confirm(`¿Desea eliminar a ${name} ${lastname}`)
 if(res) {
  try {
    const response = await fetch(`${API}`, {
      
      method: 'DELETE',
      body: JSON.stringify({ id: id }),
      headers: {
        'Content-Type': 'application/json',
      },
    });

    if (response.ok) {
      await refrescarDatos();
    } 
  } catch (error) {
    console.error("Error al eliminar:", error);
  }
 }

};

const refrescarDatos = async () => {
  try {
    const data = await fetch(API);
    usuarios.value = await data.json();
  } catch (error) {
    console.error("Error al obtener datos:", error);
  }
};

// Llama a la función refrescarDatos cuando se monta el componente
onMounted(refrescarDatos);



onMounted(async () => {
  const data = await fetch(API);
  usuarios.value = await data.json();

});


</script>

<style scoped>

</style>