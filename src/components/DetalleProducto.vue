<script setup>
defineProps({
  producto: {
    type: Object,
    default: null
  }
});

const emit = defineEmits(['cerrar']);

const handleCerrar = () => {
  emit('cerrar');
};
</script>

<template>
  <div v-if="producto" class="detalle-overlay" @click.self="handleCerrar">
    <div class="detalle-container">
      <button class="btn-cerrar" @click="handleCerrar">✕</button>

      <div class="detalle-contenido">
        <div class="imagen-detalle">
          <img :src="producto.imagen" :alt="producto.nombre" />
        </div>

        <div class="info-detalle">
          <h2>{{ producto.nombre }}</h2>

          <div class="precio-detalle">
            ${{ producto.precio.toLocaleString() }}
          </div>

          <div class="stock-detalle" :class="{ 'sin-stock': producto.stock === 0 }">
            <span v-if="producto.stock > 0">
              ✓ En stock: {{ producto.stock }} unidades disponibles
            </span>
            <span v-else>
              ✕ Producto agotado
            </span>
          </div>

          <div class="descripcion-detalle">
            <h3>Descripción</h3>
            <p>{{ producto.descripcion }}</p>
          </div>

          <div class="caracteristicas">
            <h3>Características</h3>
            <ul>
              <li>ID del producto: #{{ producto.id }}</li>
              <li>Disponibilidad inmediata</li>
              <li>Garantía incluida</li>
              <li>Envío a todo el país</li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.detalle-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.75);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
  padding: 20px;
  animation: fadeIn 0.3s ease;
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

.detalle-container {
  background: white;
  border-radius: 16px;
  max-width: 900px;
  width: 100%;
  max-height: 90vh;
  overflow-y: auto;
  position: relative;
  animation: slideUp 0.3s ease;
}

@keyframes slideUp {
  from {
    transform: translateY(30px);
    opacity: 0;
  }
  to {
    transform: translateY(0);
    opacity: 1;
  }
}

.btn-cerrar {
  position: absolute;
  top: 16px;
  right: 16px;
  width: 40px;
  height: 40px;
  border: none;
  background: white;
  border-radius: 50%;
  font-size: 24px;
  cursor: pointer;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.15);
  z-index: 10;
  transition: transform 0.2s ease, background 0.2s ease;
  display: flex;
  align-items: center;
  justify-content: center;
  color: #4a5568;
}

.btn-cerrar:hover {
  transform: scale(1.1);
  background: #f7fafc;
}

.detalle-contenido {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 40px;
  padding: 40px;
}

.imagen-detalle {
  width: 100%;
  height: 400px;
  border-radius: 12px;
  overflow: hidden;
  background: #f7fafc;
}

.imagen-detalle img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.info-detalle {
  display: flex;
  flex-direction: column;
  gap: 24px;
}

h2 {
  margin: 0;
  font-size: 32px;
  font-weight: 700;
  color: #1a202c;
}

.precio-detalle {
  font-size: 36px;
  font-weight: 700;
  color: #2c5282;
}

.stock-detalle {
  padding: 12px 16px;
  border-radius: 8px;
  font-weight: 600;
  background: #c6f6d5;
  color: #22543d;
}

.stock-detalle.sin-stock {
  background: #fed7d7;
  color: #742a2a;
}

.descripcion-detalle,
.caracteristicas {
  display: flex;
  flex-direction: column;
  gap: 12px;
}

h3 {
  margin: 0;
  font-size: 18px;
  font-weight: 600;
  color: #2d3748;
}

.descripcion-detalle p {
  margin: 0;
  color: #4a5568;
  line-height: 1.6;
}

.caracteristicas ul {
  margin: 0;
  padding-left: 20px;
  color: #4a5568;
  line-height: 1.8;
}

@media (max-width: 768px) {
  .detalle-contenido {
    grid-template-columns: 1fr;
    padding: 24px;
    gap: 24px;
  }

  .imagen-detalle {
    height: 300px;
  }

  h2 {
    font-size: 24px;
  }

  .precio-detalle {
    font-size: 28px;
  }
}
</style>
