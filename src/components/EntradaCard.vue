<template>
  <article class="card" @click="$emit('ver', animal)">
    <div class="card-img">
      <img :src="animal.imagen" :alt="animal.nombre" @error="onImgError" />
      <span class="badge" :class="categoriaClass">{{ animal.categoria }}</span>
      <span v-if="animal.audio" class="badge-audio">🔊</span>
    </div>
    <div class="card-body">
      <p class="region">{{ animal.region }}</p>
      <h3>{{ animal.nombre }}</h3>
      <p class="cientifico">{{ animal.nombreCientifico }}</p>
      <span class="conservacion" :class="conservacionClass">{{ animal.estadoConservacion }}</span>
    </div>
  </article>
</template>

<script setup>
const props = defineProps({ animal: Object })
defineEmits(['ver'])

function onImgError(e) {
  e.target.src = 'https://placehold.co/400x300/2d6a4f/white?text=' + encodeURIComponent(props.animal.nombre)
}

const categoriaClass = {
  'Ave': 'badge-ave',
  'Mamífero': 'badge-mamifero',
  'Reptil': 'badge-reptil',
  'Anfibio': 'badge-anfibio',
}[props.animal.categoria] || ''

const conservacionMap = {
  'Preocupación menor': 'estado-ok',
  'Casi amenazado': 'estado-medio',
  'Vulnerable': 'estado-medio',
  'En peligro': 'estado-peligro',
}
const conservacionClass = conservacionMap[props.animal.estadoConservacion] || ''
</script>

<style scoped>
.card {
  background: var(--card-bg);
  border-radius: 16px;
  overflow: hidden;
  cursor: pointer;
  box-shadow: 0 2px 12px rgba(0,0,0,0.08);
  transition: transform 0.2s, box-shadow 0.2s;
}
.card:hover {
  transform: translateY(-6px);
  box-shadow: 0 10px 28px rgba(0,0,0,0.15);
}
.card-img {
  position: relative;
  aspect-ratio: 4/3;
  overflow: hidden;
  background: #e8f5e9;
}
.card-img img {
  width: 100%; height: 100%;
  object-fit: cover;
  display: block;
  transition: transform 0.4s;
}
.card:hover .card-img img { transform: scale(1.06); }

.badge {
  position: absolute; top: 10px; left: 10px;
  font-size: 11px; font-weight: 700;
  padding: 3px 10px; border-radius: 99px;
  text-transform: uppercase; letter-spacing: 0.05em;
}
.badge-ave      { background: #d4edda; color: #155724; }
.badge-mamifero { background: #fff3cd; color: #856404; }
.badge-reptil   { background: #f8d7da; color: #721c24; }
.badge-anfibio  { background: #cce5ff; color: #004085; }

.badge-audio {
  position: absolute; top: 10px; right: 10px;
  font-size: 18px;
}

.card-body { padding: 14px 16px 18px; }
.region { font-size: 11px; color: var(--text-muted); text-transform: uppercase; letter-spacing: 0.06em; margin: 0 0 4px; }
h3 { margin: 0 0 3px; font-size: 1.05rem; color: var(--text); }
.cientifico { font-style: italic; font-size: 0.82rem; color: var(--text-muted); margin: 0 0 10px; }

.conservacion {
  font-size: 11px; font-weight: 600;
  padding: 3px 10px; border-radius: 99px;
}
.estado-ok     { background: #d4edda; color: #155724; }
.estado-medio  { background: #fff3cd; color: #856404; }
.estado-peligro{ background: #f8d7da; color: #721c24; }
</style>
