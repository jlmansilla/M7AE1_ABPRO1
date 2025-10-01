<script setup>
import { ref, computed } from 'vue';
import TarjetaProducto from './TarjetaProducto.vue';
import DetalleProducto from './DetalleProducto.vue';

const productos = ref([
  {
    id: 1,
    nombre: 'Laptop HP Pavilion',
    precio: 899990,
    imagen: 'https://images.pexels.com/photos/18105/pexels-photo.jpg?auto=compress&cs=tinysrgb&w=800',
    stock: 8,
    descripcion: 'Laptop potente con procesador Intel Core i7, 16GB RAM y 512GB SSD. Perfecta para trabajo y entretenimiento.'
  },
  {
    id: 2,
    nombre: 'Mouse Inalámbrico',
    precio: 29990,
    imagen: 'https://images.pexels.com/photos/2115257/pexels-photo-2115257.jpeg?auto=compress&cs=tinysrgb&w=800',
    stock: 3,
    descripcion: 'Mouse ergonómico inalámbrico con precisión de 1600 DPI. Batería de larga duración.'
  },
  {
    id: 3,
    nombre: 'Teclado Mecánico RGB',
    precio: 79990,
    imagen: 'https://images.pexels.com/photos/1772123/pexels-photo-1772123.jpeg?auto=compress&cs=tinysrgb&w=800',
    stock: 0,
    descripcion: 'Teclado mecánico con switches azules, retroiluminación RGB personalizable y diseño compacto.'
  },
  {
    id: 4,
    nombre: 'Monitor 27" 4K',
    precio: 449990,
    imagen: 'https://images.pexels.com/photos/1779487/pexels-photo-1779487.jpeg?auto=compress&cs=tinysrgb&w=800',
    stock: 12,
    descripcion: 'Monitor 4K UHD de 27 pulgadas con tecnología IPS, frecuencia de 60Hz y soporte VESA.',
    esOferta: true,
    etiqueta: '15% OFF'
  },
  {
    id: 5,
    nombre: 'Auriculares Bluetooth',
    precio: 129990,
    imagen: 'https://images.pexels.com/photos/3394650/pexels-photo-3394650.jpeg?auto=compress&cs=tinysrgb&w=800',
    stock: 15,
    descripcion: 'Auriculares inalámbricos con cancelación de ruido activa, hasta 30 horas de batería.'
  },
  {
    id: 6,
    nombre: 'Webcam Full HD',
    precio: 59990,
    imagen: 'https://images.pexels.com/photos/5797903/pexels-photo-5797903.jpeg?auto=compress&cs=tinysrgb&w=800',
    stock: 6,
    descripcion: 'Webcam 1080p con micrófono incorporado y enfoque automático. Ideal para videollamadas.',
    esOferta: true,
    etiqueta: 'RECOMENDADO'
  }
]);

const carrito = ref([]);
const productoSeleccionado = ref(null);
const componenteActivo = ref(null);

const cantidadCarrito = computed(() => carrito.value.length);

const agregarAlCarrito = (id) => {
  carrito.value.push(id);
  console.log(`Producto ${id} agregado al carrito. Total items: ${cantidadCarrito.value}`);
};

const verDetalle = (producto) => {
  productoSeleccionado.value = producto;
  componenteActivo.value = DetalleProducto;
};

const cerrarDetalle = () => {
  productoSeleccionado.value = null;
  componenteActivo.value = null;
};

const vaciarCarrito = () => {
  carrito.value = [];
  console.log('Carrito vaciado');
};
</script>

<template>
  <div class="catalogo-container">
    <header class="catalogo-header">
      <div class="header-content">
        <h1>Catálogo de Productos</h1>
        <p class="subtitle">Encuentra los mejores productos de tecnología</p>
      </div>

      <div class="carrito-badge">
        <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
          <circle cx="9" cy="21" r="1"/>
          <circle cx="20" cy="21" r="1"/>
          <path d="M1 1h4l2.68 13.39a2 2 0 0 0 2 1.61h9.72a2 2 0 0 0 2-1.61L23 6H6"/>
        </svg>
        <span class="badge-count" v-if="cantidadCarrito > 0">{{ cantidadCarrito }}</span>
        <button v-if="cantidadCarrito > 0" @click="vaciarCarrito" class="btn-vaciar">
          Vaciar
        </button>
      </div>
    </header>

    <div class="productos-grid">
      <TarjetaProducto
        v-for="producto in productos"
        :key="producto.id"
        :id="producto.id"
        :nombre="producto.nombre"
        :precio="producto.precio"
        :imagen="producto.imagen"
        :stock="producto.stock"
        :descripcion="producto.descripcion"
        @agregar-al-carrito="agregarAlCarrito"
        @click="verDetalle(producto)"
      >
        <div v-if="producto.esOferta" class="etiqueta-personalizada">
          {{ producto.etiqueta }}
        </div>
      </TarjetaProducto>
    </div>

    <component
      :is="componenteActivo"
      v-if="componenteActivo && productoSeleccionado"
      :producto="productoSeleccionado"
      @cerrar="cerrarDetalle"
    />
  </div>
</template>

<style scoped>
.catalogo-container {
  min-height: 100vh;
  background: linear-gradient(135deg, #f5f7fa 0%, #e8eef3 100%);
  padding: 32px 24px;
}

.catalogo-header {
  max-width: 1200px;
  margin: 0 auto 48px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  gap: 24px;
}

.header-content h1 {
  margin: 0 0 8px 0;
  font-size: 42px;
  font-weight: 700;
  color: #1a202c;
  background: linear-gradient(135deg, #2c5282 0%, #1a365d 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.subtitle {
  margin: 0;
  font-size: 18px;
  color: #4a5568;
}

.carrito-badge {
  display: flex;
  align-items: center;
  gap: 16px;
  padding: 16px 24px;
  background: white;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  position: relative;
}

.carrito-badge svg {
  color: #2c5282;
}

.badge-count {
  position: absolute;
  top: 8px;
  right: 8px;
  background: #e53e3e;
  color: white;
  border-radius: 50%;
  width: 24px;
  height: 24px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 12px;
  font-weight: 700;
}

.btn-vaciar {
  padding: 8px 16px;
  background: #e53e3e;
  color: white;
  border: none;
  border-radius: 8px;
  font-size: 14px;
  font-weight: 600;
  cursor: pointer;
  transition: background 0.3s ease;
}

.btn-vaciar:hover {
  background: #c53030;
}

.productos-grid {
  max-width: 1200px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 32px;
}

.etiqueta-personalizada {
  margin-top: 12px;
  padding: 8px 16px;
  background: linear-gradient(135deg, #48bb78 0%, #38a169 100%);
  color: white;
  text-align: center;
  border-radius: 8px;
  font-weight: 700;
  font-size: 14px;
  letter-spacing: 0.5px;
  text-transform: uppercase;
  box-shadow: 0 2px 4px rgba(72, 187, 120, 0.3);
}

@media (max-width: 768px) {
  .catalogo-container {
    padding: 24px 16px;
  }

  .catalogo-header {
    flex-direction: column;
    align-items: flex-start;
    margin-bottom: 32px;
  }

  .header-content h1 {
    font-size: 32px;
  }

  .subtitle {
    font-size: 16px;
  }

  .productos-grid {
    grid-template-columns: 1fr;
    gap: 24px;
  }

  .carrito-badge {
    width: 100%;
    justify-content: space-between;
  }
}
</style>
