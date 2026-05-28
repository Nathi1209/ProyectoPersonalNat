<template>
  <div class="overlay" @click.self="$emit('cerrar')">
    <div class="modal">
      <button class="btn-cerrar" @click="$emit('cerrar')">✕</button>

      <div class="modal-img">
        <img :src="animal.imagen" :alt="animal.nombre" @error="onImgError" />
      </div>

      <div class="modal-body">
        <span class="badge" :class="categoriaClass">{{ animal.categoria }}</span>
        <h2>{{ animal.nombre }}</h2>
        <p class="cientifico">{{ animal.nombreCientifico }}</p>

        <div class="info-grid">
          <div class="info-item">
            <span class="info-label">Región</span>
            <span>{{ animal.region }}</span>
          </div>
          <div class="info-item">
            <span class="info-label">Hábitat</span>
            <span>{{ animal.habitat }}</span>
          </div>
          <div class="info-item">
            <span class="info-label">Estado de conservación</span>
            <span class="conservacion" :class="conservacionClass">{{ animal.estadoConservacion }}</span>
          </div>
        </div>

        <p class="descripcion">{{ animal.descripcion }}</p>

        <div class="curiosidad">
          <span class="curiosidad-icon">💡</span>
          <p>{{ animal.curiosidad }}</p>
        </div>

        <div v-if="animal.audio" class="audio-section">
          <p class="audio-label">Narración de audio</p>
          <audio controls :src="animal.audio">Tu navegador no soporta audio.</audio>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const props = defineProps({ animal: Object })
defineEmits(['cerrar'])

function onImgError(e) {
  e.target.src = 'https://placehold.co/600x400/2d6a4f/white?text=' + encodeURIComponent(props.animal.nombre)
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
.overlay {
  position: fixed; inset: 0; z-index: 100;
  background: rgba(0,0,0,0.6);
  display: flex; align-items: center; justify-content: center;
  padding: 20px;
}
.modal {
  background: var(--card-bg);
  border-radius: 20px;
  max-width: 620px; width: 100%;
  max-height: 90vh; overflow-y: auto;
  position: relative;
}
.btn-cerrar {
  position: sticky; top: 10px; left: 100%;
  margin: 12px 12px 0 0;
  background: var(--bg); border: none;
  width: 34px; height: 34px; border-radius: 50%;
  font-size: 16px; cursor: pointer; color: var(--text);
  display: flex; align-items: center; justify-content: center;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
  float: right;
}
.btn-cerrar:hover { background: #f8d7da; color: #721c24; }

.modal-img { aspect-ratio: 16/9; overflow: hidden; }
.modal-img img { width: 100%; height: 100%; object-fit: cover; display: block; }

.modal-body { padding: 20px 24px 28px; }

.badge {
  font-size: 11px; font-weight: 700;
  padding: 3px 10px; border-radius: 99px;
  text-transform: uppercase; letter-spacing: 0.05em;
  display: inline-block; margin-bottom: 8px;
}
.badge-ave      { background: #d4edda; color: #155724; }
.badge-mamifero { background: #fff3cd; color: #856404; }
.badge-reptil   { background: #f8d7da; color: #721c24; }
.badge-anfibio  { background: #cce5ff; color: #004085; }

h2 { margin: 0 0 4px; font-size: 1.5rem; color: var(--text); }
.cientifico { font-style: italic; color: var(--text-muted); margin: 0 0 16px; }

.info-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 12px; margin-bottom: 16px; }
.info-item { display: flex; flex-direction: column; gap: 3px; }
.info-label { font-size: 10px; font-weight: 700; text-transform: uppercase; letter-spacing: 0.06em; color: var(--text-muted); }

.conservacion {
  font-size: 12px; font-weight: 600;
  padding: 2px 8px; border-radius: 99px; display: inline-block;
}
.estado-ok     { background: #d4edda; color: #155724; }
.estado-medio  { background: #fff3cd; color: #856404; }
.estado-peligro{ background: #f8d7da; color: #721c24; }

.descripcion { line-height: 1.7; color: var(--text); margin-bottom: 16px; }

.curiosidad {
  background: var(--bg);
  border-radius: 12px; padding: 14px 16px;
  display: flex; gap: 10px; align-items: flex-start;
  margin-bottom: 16px;
}
.curiosidad-icon { font-size: 20px; flex-shrink: 0; }
.curiosidad p { margin: 0; font-size: 0.9rem; color: var(--text); line-height: 1.6; }

.audio-section { margin-top: 8px; }
.audio-label { font-size: 12px; font-weight: 600; color: var(--text-muted); margin-bottom: 6px; text-transform: uppercase; letter-spacing: 0.05em; }
audio { width: 100%; border-radius: 8px; }
</style>
