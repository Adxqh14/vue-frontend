<script setup>
import { ref, onMounted } from 'vue';
import AppSidebar from './components/AppSidebar.vue';
import Ola from './components/ola.vue';



// Creamos una variable reactiva para guardar los usuarios
const usuarios = ref([]);

// Traemos los datos al montar el componente
onMounted(async () => {
  try {
    const res = await fetch('http://localhost:vue-backend-production.up.railway.app');
    const data = await res.json();
    usuarios.value = data; // Actualizamos la variable reactiva
  } catch (err) {
    console.error('Error al traer datos:', err);
  }
});
</script>

<template>
  <header>
    <AppSidebar />
    <Ola/>
  </header>
 <main class="flex flex-col min-h-screen bg-gray-100">
  

  <div class="flex-1 flex flex-col items-center justify-center p-8">
    <h1 class="text-4xl font-bold text-blue-600 mb-8">
      ¡Mi gran tripulación!
    </h1>

    <ul class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
      <li
        v-for="user in usuarios"
        :key="user.id"
        class="bg-gradient-to-br from-white to-gray-50 p-5 rounded-3xl shadow-lg hover:shadow-xl transition-all transform hover:-translate-y-1"
      >
        <h3 class="text-xl font-semibold text-gray-700 mb-2">{{ user.nombre }}</h3>
        <p class="text-sm text-gray-500">ID: {{ user.id }}</p>
        <p class="text-sm text-gray-500">Puesto: {{ user.puesto }}</p>
        <p class="text-sm text-gray-500">Bounty: {{ user.bounty }}</p>
      </li>
    </ul>
  </div>
</main>

</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
