<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <div class="max-w-md mx-auto p-4 border rounded shadow">
    <h2 class="text-xl font-bold mb-4">Agregar miembro de la tripulación</h2>
    <form @submit.prevent="handleSubmit" class="space-y-3">
      <div>
        <label>Nombre:</label>
        <input v-model="nombre" type="text" class="w-full border px-2 py-1 rounded"/>
      </div>
      <div>
        <label>Puesto:</label>
        <input v-model="puesto" type="text" class="w-full border px-2 py-1 rounded"/>
      </div>
      <div>
        <label>Bounty:</label>
        <input v-model.number="bounty" type="number" class="w-full border px-2 py-1 rounded"/>
      </div>
      <button type="submit" class="bg-blue-500 text-white px-4 py-2 rounded hover:bg-blue-600">Agregar</button>
    </form>
    <p v-if="mensaje" class="mt-3">{{ mensaje }}</p>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const nombre = ref('')
const puesto = ref('')
const bounty = ref('')
const mensaje = ref('')

const handleSubmit = async () => {
  if (!nombre.value || !puesto.value || !bounty.value) {
    mensaje.value = '❌ Completa todos los campos'
    return
  }

  try {
    const res = await fetch('http://localhost:4001/thousandsunny', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({
        nombre: nombre.value,
        puesto: puesto.value,
        bounty: bounty.value
      })
    })

    const data = await res.json()

    if (res.ok) {
      mensaje.value = `✅ ${data.message}`
      nombre.value = ''
      puesto.value = ''
      bounty.value = ''
    } else {
      mensaje.value = `❌ ${data.error}: ${data.details || ''}`
    }
  } catch (err) {
    console.error(err)
    mensaje.value = '❌ Error al conectar con el servidor'
  }
}
</script>
