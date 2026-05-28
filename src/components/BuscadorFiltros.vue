<template>
  <div class="buscador-wrap">
    <div class="search-box">
      <span class="search-icon">🔍</span>
      <input
        type="text"
        placeholder="Buscar animal..."
        :value="busqueda"
        @input="$emit('update:busqueda', $event.target.value)"
      />
    </div>

    <div class="filtros">
      <button
        v-for="cat in categorias"
        :key="cat"
        class="filtro-btn"
        :class="{ activo: categoriaActiva === cat }"
        @click="$emit('update:categoriaActiva', categoriaActiva === cat ? '' : cat)"
      >
        {{ iconos[cat] || '🐾' }} {{ cat }}
      </button>
    </div>
  </div>
</template>

<script setup>
defineProps({
  busqueda: String,
  categoriaActiva: String,
})
defineEmits(['update:busqueda', 'update:categoriaActiva'])

const categorias = ['Ave', 'Mamífero', 'Reptil', 'Anfibio']
const iconos = {
  'Ave': '🦜',
  'Mamífero': '🦥',
  'Reptil': '🐍',
  'Anfibio': '🐸',
}
</script>

<style scoped>
.buscador-wrap {
  display: flex; flex-direction: column; gap: 12px;
  margin-bottom: 28px;
}
.search-box {
  position: relative; max-width: 420px;
}
.search-icon {
  position: absolute; left: 14px; top: 50%; transform: translateY(-50%);
  font-size: 16px; pointer-events: none;
}
input {
  width: 100%; padding: 12px 16px 12px 42px;
  border: 2px solid var(--border);
  border-radius: 12px; font-size: 0.95rem;
  background: var(--card-bg); color: var(--text);
  outline: none; box-sizing: border-box;
  transition: border-color 0.2s;
}
input:focus { border-color: var(--verde); }

.filtros { display: flex; gap: 8px; flex-wrap: wrap; }
.filtro-btn {
  padding: 7px 16px; border-radius: 99px;
  border: 2px solid var(--border);
  background: var(--card-bg); color: var(--text);
  font-size: 0.85rem; cursor: pointer; font-weight: 500;
  transition: all 0.2s;
}
.filtro-btn:hover { border-color: var(--verde); }
.filtro-btn.activo {
  background: var(--verde); color: #fff; border-color: var(--verde);
}
</style>
