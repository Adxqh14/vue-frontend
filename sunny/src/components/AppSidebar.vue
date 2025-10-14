<!-- src/components/AppSidebar.vue -->
<template>
  <aside
    class="w-64 min-h-screen bg-white border-r shadow-md flex flex-col fixed md:static z-50"
  >
    <!-- Header -->
    <div class="p-4 border-b flex items-center justify-center">
      <h2 class="text-2xl font-bold text-blue-600">Sunny Corp</h2>
    </div>

    <!-- Navegación principal -->
    <nav class="flex  p-4 space-y-2">
      <a
        v-for="item in menuItems"
        :key="item.title"
        :href="item.url"
        class="flex items-center gap-3 p-2 rounded-lg text-gray-700 hover:bg-blue-50 hover:text-blue-600 transition-all"
      >
        <component :is="item.icon" class="w-5 h-5" />
        <span class="font-medium">{{ item.title }}</span>
      </a>
    </nav>

    <!-- Usuario (footer) -->
    <div class="p-4 border-t flex items-center gap-3">
      <img
        :src="user.avatar"
        alt="avatar"
        class="w-10 h-10 rounded-full border"
      />
      <div>
        <p class="font-semibold">{{ user.name }}</p>
        <p class="text-sm text-gray-500">{{ user.email }}</p>
      </div>
    </div>
  </aside>
</template>

<script setup>
import { IconHome, IconList, IconUsers, IconChartBar, IconSettings } from '@tabler/icons-vue'

// Datos del usuario
const user = {
  name: 'Monkey D. Luffy',
  email: 'luffy@onepiece.com',
  avatar: 'https://i.pravatar.cc/100?img=2',
}

// Ítems del menú
const menuItems = [
  { title: 'Inicio', url: '#', icon: IconHome },
  { title: 'Inventario', url: '#', icon: IconList },
  { title: 'Ventas', url: '#', icon: IconChartBar },
  { title: 'Clientes', url: '#', icon: IconUsers },
  { title: 'Configuración', url: '#', icon: IconSettings },
]
</script>

<style scoped>
aside {
  transition: all 0.3s ease;
}
</style>
