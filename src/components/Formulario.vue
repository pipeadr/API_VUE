<template>
    <h1>{{ user ? 'editar' : 'Agregar' }} Usuario</h1>
        <form  @submit.prevent="procesarForm"  class="row g-3 needs-validation" novalidate>
            <div class="col-md-4">
                <label for="validationCustom01" class="form-label">Nombre</label>
                <input type="text" class="form-control"  name="name" id="validationCustom01" placeholder="nombre" required  v-model="formData.name">
                <div class="valid-feedback">
                Looks good!
                </div>
           </div>

           <div class="col-md-4">
                <label for="validationCustom01" class="form-label">Apellido</label>
                <input type="text" class="form-control"  name="lastname" id="validationCustom01" placeholder="apellido" required v-model="formData.lastname">
                <div class="valid-feedback">
                Looks good!
                </div>
           </div>


           <div class="col-md-4">
                <label for="validationCustom01" class="form-label">Correo</label>
                
                <input type="email" class="form-control"  id="validationCustom01" name="email" placeholder="nombre@ejemplo.com" required v-model="formData.email">
                <div class="valid-feedback">
                Looks good!
                </div>
           </div>

           <div class="col-12">
              <button class="btn btn-primary" :disabled="cargando" >Enviar</button>
            </div>
            
            <div v-if="mostrarError" class="error-message">Por favor, complete todos los campos.</div>
        </form>
        <!-- {{ user }}
        {{ formData }} -->
   
</template>

<script setup lang="ts">
import {computed, onMounted, reactive, ref, watch} from "vue";
import { useRoute, useRouter } from 'vue-router';
import { API } from "@/constantes";
import type { ITarea } from "@/constantes";
const tareas = ref<ITarea[]>([]);

// const {user} = defineProps({
    const props = defineProps({
    user: {
        type: Object as () => ITarea || null,
        default: null
    }
}) 


// const formData = reactive({
//     id: user?.id ?? null,
//     name: user?.name ?? '',
//     lastname: user?.lastname ?? '',
//     email: user?.email ??''
// })

const formData = reactive({
    id: '',
    name:  '',
    lastname:  '',
    email: ''
})

const cargando = ref(false)
const mostrarError = ref(false); 
 const router = useRouter()
const user = computed(() => props.user)
watch(user, ()=> {
    console.log("ayudaaa")
    const firstUser = user.value[0];
    // console.log(firstUser.email)
    console.log(firstUser.id)
    formData.id = firstUser.id
    formData.name = firstUser.name
    formData.lastname = firstUser.lastname
    formData.email = firstUser.email
    
    
})

const procesarForm = async() => {
    if (!formData.name || !formData.lastname || !formData.email) {
    // Mostrar un mensaje de error y evitar que se envíe el formulario
    mostrarError.value = true;
    return;
  }
     cargando.value = true;
     if(formData.name )
     if(user.value) {
        await fetch(`${API}`, {
        method: 'PUT',
        body: JSON.stringify({nombre:formData.name, apellido:formData.lastname, correo:formData.email, id: formData.id}),
         headers:{
        'Content-Type': 'application/json'
      }
     })
     } else {
        await fetch(`${API}`, {
        method: 'POST',
        body: JSON.stringify({nombre:formData.name, apellido:formData.lastname, correo:formData.email}),
         headers:{
        'Content-Type': 'application/json'
      }
     })
     }

     cargando.value = false
     router.push("/tareas");
     
}

</script>

<style scoped>

</style>