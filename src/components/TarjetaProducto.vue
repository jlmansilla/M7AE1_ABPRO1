<script setup>
import { onBeforeMount, onMounted, onBeforeUnmount } from 'vue';

const props = defineProps({
  id: {
    type: Number,
    required: true
  },
  nombre: {
    type: String,
    required: true
  },
  precio: {
    type: Number,
    required: true
  },
  imagen: {
    type: String,
    required: true
  },
  stock: {
    type: Number,
    required: true
  },
  descripcion: {
    type: String,
    required: true
  }
});

const emit = defineEmits(['agregarAlCarrito']);

onBeforeMount(() => {
  console.log(`[TarjetaProducto ${props.id}] - beforeMount: Componente a punto de montarse`);
});

onMounted(() => {
  console.log(`[TarjetaProducto ${props.id}] - mounted: Componente montado y listo`);
});

onBeforeUnmount(() => {
  console.log(`[TarjetaProducto ${props.id}] - beforeUnmount: Componente a punto de destruirse`);
});

const handleAgregarCarrito = () => {
  emit('agregarAlCarrito', props.id);
};
</script>

<template>
  <div
    class="tarjeta-producto"
    :class="{ 'sin-stock': stock === 0 }"
  >
    <div class="imagen-container">
      <img :src="imagen" :alt="nombre" />
      <div v-if="stock === 0" class="badge-agotado">Agotado</div>
      <div v-else-if="stock < 5" class="badge-pocas-unidades">Pocas unidades</div>
    </div>

    <div class="contenido">
      <h3>{{ nombre }}</h3>
      <p class="descripcion">{{ descripcion }}</p>

      <div class="info-producto">
        <p class="precio" :style="{ color: stock === 0 ? '#999' : '#2c5282' }">
          ${{ precio.toLocaleString() }}
        </p>
        <p class="stock">Stock: {{ stock }}</p>
      </div>

      <button
        @click="handleAgregarCarrito"
        :disabled="stock === 0"
        class="btn-agregar"
      >
        {{ stock === 0 ? 'No disponible' : 'Agregar al carrito' }}
      </button>

      <slot></slot>
    </div>
  </div>
</template>

<style scoped>
.tarjeta-producto {
  background: white;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  overflow: hidden;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  display: flex;
  flex-direction: column;
  height: 100%;
}

.tarjeta-producto:hover {
  transform: translateY(-4px);
  box-shadow: 0 4px 16px rgba(0, 0, 0, 0.15);
}

.tarjeta-producto.sin-stock {
  opacity: 0.7;
}

.imagen-container {
  position: relative;
  width: 100%;
  height: 240px;
  overflow: hidden;
  background: #f7fafc;
}

.imagen-container img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.3s ease;
}

.tarjeta-producto:hover .imagen-container img {
  transform: scale(1.05);
}

.badge-agotado,
.badge-pocas-unidades {
  position: absolute;
  top: 12px;
  right: 12px;
  padding: 6px 12px;
  border-radius: 6px;
  font-size: 12px;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.badge-agotado {
  background: #e53e3e;
  color: white;
}

.badge-pocas-unidades {
  background: #ed8936;
  color: white;
}

.contenido {
  padding: 20px;
  display: flex;
  flex-direction: column;
  flex: 1;
}

h3 {
  margin: 0 0 12px 0;
  font-size: 20px;
  font-weight: 600;
  color: #1a202c;
}

.descripcion {
  margin: 0 0 16px 0;
  color: #4a5568;
  font-size: 14px;
  line-height: 1.5;
  flex: 1;
}

.info-producto {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 16px;
}

.precio {
  font-size: 24px;
  font-weight: 700;
  margin: 0;
}

.stock {
  margin: 0;
  color: #718096;
  font-size: 14px;
}

.btn-agregar {
  width: 100%;
  padding: 12px;
  background: #2c5282;
  color: white;
  border: none;
  border-radius: 8px;
  font-size: 16px;
  font-weight: 600;
  cursor: pointer;
  transition: background 0.3s ease, transform 0.1s ease;
}

.btn-agregar:hover:not(:disabled) {
  background: #2a4365;
  transform: scale(1.02);
}

.btn-agregar:active:not(:disabled) {
  transform: scale(0.98);
}

.btn-agregar:disabled {
  background: #cbd5e0;
  cursor: not-allowed;
}
</style>
