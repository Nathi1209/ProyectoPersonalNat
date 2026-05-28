<template>
  <div :class="{ 'dark': modoOscuro }">
    <!-- Header -->
    <header class="site-header">
      <div class="header-content">
        <div class="header-titulo">
          <span class="header-emoji">🦜</span>
          <div>
            <h1>Animales de Costa Rica</h1>
            <p>Enciclopedia de fauna silvestre</p>
          </div>
        </div>
        <button class="btn-modo" @click="modoOscuro = !modoOscuro" :title="modoOscuro ? 'Modo claro' : 'Modo oscuro'">
          {{ modoOscuro ? '☀️' : '🌙' }}
        </button>
      </div>
    </header>

    <!-- Contenido principal -->
    <main class="main-content">

      <!-- Buscador y filtros -->
      <BuscadorFiltros
        v-model:busqueda="busqueda"
        v-model:categoriaActiva="categoriaActiva"
      />

      <!-- Contador resultados -->
      <p class="contador">
        {{ animalesFiltrados.length }} resultado{{ animalesFiltrados.length !== 1 ? 's' : '' }}
      </p>

      <!-- Grid de tarjetas -->
      <div v-if="animalesFiltrados.length > 0" class="grid">
        <EntradaCard
          v-for="animal in animalesFiltrados"
          :key="animal.id"
          :animal="animal"
          @ver="abrirDetalle"
        />
      </div>

      <!-- Sin resultados -->
      <div v-else class="sin-resultados">
        <p>🔎 No se encontraron animales con ese criterio.</p>
      </div>
    </main>

    <!-- Modal de detalle -->
    <DetalleModal
      v-if="animalSeleccionado"
      :animal="animalSeleccionado"
      @cerrar="animalSeleccionado = null"
    />
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import animalesData from './data/animales.json'
import EntradaCard from './components/EntradaCard.vue'
import BuscadorFiltros from './components/BuscadorFiltros.vue'
import DetalleModal from './components/DetalleModal.vue'

const modoOscuro = ref(false)
const busqueda = ref('')
const categoriaActiva = ref('')
const animalSeleccionado = ref(null)

const animalesFiltrados = computed(() => {
  return animalesData.filter(animal => {
    const coincideBusqueda = busqueda.value === '' ||
      animal.nombre.toLowerCase().includes(busqueda.value.toLowerCase()) ||
      animal.nombreCientifico.toLowerCase().includes(busqueda.value.toLowerCase()) ||
      animal.region.toLowerCase().includes(busqueda.value.toLowerCase())

    const coincideCategoria = categoriaActiva.value === '' ||
      animal.categoria === categoriaActiva.value

    return coincideBusqueda && coincideCategoria
  })
})

function abrirDetalle(animal) {
  animalSeleccionado.value = animal
}
</script>

<style>
/* Las variables y el layout global van en style.css */
</style>
