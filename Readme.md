# 🦜 Animales de Costa Rica — Enciclopedia Interactiva

Proyecto personal desarrollado para el curso **IF7102 Lenguajes para Aplicaciones Comerciales**.

## Framework elegido
**Vue 3** — Composition API con Single File Components (.vue)  
Declarado en el primer commit del repositorio (28 de mayo de 2026).

## Opción elegida
**Opción 4: Enciclopedia Temática Interactiva**

## Descripción
Enciclopedia web interactiva de la fauna silvestre de Costa Rica. El usuario puede explorar 10 animales representativos del país, con información científica, hábitat, estado de conservación, galería de imágenes y narración de audio para 3 especies.

## Características implementadas
- Carga dinámica de datos desde archivo JSON (`animales.json`)
- Búsqueda en tiempo real por nombre, nombre científico o región
- Filtros por categoría: Aves, Mamíferos, Reptiles, Anfibios
- Modal de detalle con descripción completa, hábitat y estado de conservación
- Narración de audio para: Lapa Roja, Perezoso y Jaguar
- Modo oscuro / modo claro con persistencia visual
- Diseño responsivo adaptado a móvil y escritorio
- Indicadores de estado de conservación por color

## Animales incluidos
| # | Animal | Categoría | Estado |
|---|--------|-----------|--------|
| 1 | Lapa Roja | Ave | Preocupación menor |
| 2 | Perezoso de Tres Dedos | Mamífero | Preocupación menor |
| 3 | Tucán Pico Iris | Ave | Preocupación menor |
| 4 | Tortuga Baula | Reptil | Vulnerable |
| 5 | Pizote | Mamífero | Preocupación menor |
| 6 | Rana Dardo Venenosa | Anfibio | Preocupación menor |
| 7 | Jaguar | Mamífero | Casi amenazado |
| 8 | Armadillo Común | Mamífero | Preocupación menor |
| 9 | Mono Carablanca | Mamífero | Preocupación menor |
| 10 | Serpiente Terciopelo | Reptil | Preocupación menor |

## Tecnologías
| Tecnología | Versión | Uso |
|-----------|---------|-----|
| Vue 3 | 3.5.13 | Framework principal — Composition API |
| Vite | 6.3.5 | Bundler y servidor de desarrollo |
| JavaScript | ES2022 | Lógica de la aplicación |
| CSS3 | — | Estilos, variables de tema y responsividad |

## Uso de Inteligencia Artificial
Los audios de narración fueron generados con herramientas de IA (síntesis de voz). Los guiones fueron redactados manualmente. Ver sección de audios en [REFERENCIAS.md](./REFERENCIAS.md).

## Cómo ejecutar
```bash
npm install
npm run dev
```
Abrir en el navegador: `http://localhost:5173`

## Estructura del proyecto
```
ProyectoPersonalNat/
├── src/
│   ├── components/
│   │   ├── EntradaCard.vue      # Tarjeta resumen de cada animal
│   │   ├── DetalleModal.vue     # Modal con información completa
│   │   └── BuscadorFiltros.vue  # Barra de búsqueda y filtros
│   ├── data/
│   │   └── animales.json        # Base de datos de los 10 animales
│   ├── imagenes/                # Fotografías de los animales
│   ├── assets/audio/            # Narración de audio (IA)
│   ├── App.vue                  # Componente raíz
│   ├── main.js                  # Punto de entrada
│   └── style.css                # Estilos globales y variables
├── REFERENCIAS.md               # Fuentes, licencias y justificación de IA
├── index.html
└── package.json
```

## Referencias
Ver archivo [REFERENCIAS.md](./REFERENCIAS.md) para fuentes de imágenes, textos y audios.

---
*Estudiante: Nathalie — IF7102 Lenguajes para Aplicaciones Comerciales, 2026*
