<template>
      <nav class="navbar navbar-expand-lg bg-body-tertiary">
        <div class="container-fluid">
            <h3 class="navbar-brand" >Navbar</h3>
            <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
            </button>
            <div class="collapse navbar-collapse" id="navbarNav">
                <ul class="navbar-nav">
                    <li class="nav-item"><RouterLink class="nav-link" to="/" exact-active-class="activo">Home</RouterLink></li>
                    <li class="nav-item"><RouterLink class="nav-link" to="/tareas" exact-active-class="activo">Tareas</RouterLink></li>
                    <li class="nav-item"><RouterLink class="nav-link" to="/tareas-formulario" exact-active-class="activo">Formulario</RouterLink></li>
                </ul>
            </div>
        </div>



      </nav>
</template>

<script setup lang="ts">
 import {RouterLink} from "vue-router";
</script>

<style scoped>
.activo {
    color: darkred;
}
</style>

