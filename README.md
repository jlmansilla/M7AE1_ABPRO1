# 🛒 Catálogo de Productos - Vue 3

Aplicación web moderna de catálogo de productos desarrollada con **Vue 3** utilizando la **Composition API** y **Vite** como bundler. Este proyecto demuestra el uso de componentes reutilizables, manejo de estado reactivo, ciclo de vida de componentes, y comunicación entre componentes padre e hijo.

## 🚀 Características

- ✅ **Vue 3 Composition API** con `<script setup>`
- 🎨 **Interfaz moderna y responsive** con diseño adaptable a móviles
- 🛍️ **Catálogo de productos** con 6 productos de tecnología
- 🛒 **Carrito de compras** funcional con contador de items
- 🔍 **Vista detallada** de productos en modal
- 📊 **Gestión de stock** con indicadores visuales
- 🏷️ **Etiquetas personalizadas** (ofertas, recomendados)
- 🎯 **Slots** para contenido personalizable
- 🔄 **Lifecycle hooks** con mensajes en consola
- 📱 **Diseño responsive** con grid adaptativo

## 🎯 Funcionalidades

### 1. Catálogo de Productos
- Grid responsive que se adapta a diferentes tamaños de pantalla
- Tarjetas de productos con:
  - Imagen del producto
  - Nombre y descripción
  - Precio formateado en pesos chilenos
  - Stock disponible
  - Badges de estado (Agotado, Pocas unidades)
  - Botón para agregar al carrito

### 2. Carrito de Compras
- Contador visual de productos en el carrito
- Badge con número de items
- Botón para vaciar el carrito
- Mensajes en consola para seguimiento

### 3. Detalle del Producto
- Modal con información completa del producto
- Vista ampliada de la imagen
- Precio destacado
- Estado de stock
- Lista de características
- Animaciones suaves de entrada/salida

### 4. Gestión de Stock
- Productos con stock limitado muestran badge "Pocas unidades" (stock < 5)
- Productos agotados se marcan visualmente
- Botón de compra deshabilitado cuando no hay stock

## 📦 Componentes

### `App.vue`
Componente raíz que renderiza el catálogo principal.

### `CatalogoProductos.vue`
Componente principal que gestiona:
- Lista de productos
- Estado del carrito
- Vista de detalle
- Lógica de negocio principal

### `TarjetaProducto.vue`
Componente reutilizable para cada producto que:
- Muestra información del producto
- Implementa lifecycle hooks (beforeMount, mounted, beforeUnmount)
- Emite eventos para agregar al carrito
- Acepta slots para contenido personalizado

### `DetalleProducto.vue`
Modal que muestra información detallada:
- Vista ampliada del producto
- Información completa
- Características adicionales
- Overlay con cierre por click o botón

## 🛠️ Tecnologías Utilizadas

- **Vue 3.4.38** - Framework JavaScript progresivo
- **Vite 5.4.2** - Build tool y dev server ultrarrápido
- **@vitejs/plugin-vue 5.1.3** - Plugin oficial de Vite para Vue
- **JavaScript (ES6+)** - Lenguaje de programación
- **CSS3** - Estilos con gradientes, animaciones y grid layout

## 📋 Requisitos Previos

- Node.js (versión 16 o superior)
- npm o yarn

## 🔧 Instalación

1. Clona el repositorio:
```bash
git clone <url-del-repositorio>
cd M7AE1_ABPRO1
```

2. Instala las dependencias:
```bash
npm install
```

## 🚀 Uso

### Modo Desarrollo
Inicia el servidor de desarrollo con hot-reload:
```bash
npm run dev
```
La aplicación estará disponible en `http://localhost:5173`

### Build para Producción
Genera la versión optimizada para producción:
```bash
npm run build
```
Los archivos compilados se generarán en la carpeta `dist/`

### Vista Previa de Producción
Previsualiza la build de producción localmente:
```bash
npm run preview
```

## 📂 Estructura del Proyecto

```
M7AE1_ABPRO1/
├── public/
│   └── vite.svg
├── src/
│   ├── assets/
│   │   └── vue.svg
│   ├── components/
│   │   ├── CatalogoProductos.vue    # Componente principal del catálogo
│   │   ├── TarjetaProducto.vue      # Tarjeta individual de producto
│   │   ├── DetalleProducto.vue      # Modal de detalle del producto
│   │   └── HelloWorld.vue           # Componente de ejemplo
│   ├── App.vue                       # Componente raíz
│   ├── main.js                       # Punto de entrada
│   └── style.css                     # Estilos globales
├── index.html                        # HTML principal
├── package.json                      # Dependencias y scripts
├── vite.config.js                    # Configuración de Vite
└── README.md                         # Este archivo
```

## 🎨 Características Técnicas

### Composition API
Utiliza la Composition API de Vue 3 con `<script setup>` para una sintaxis más concisa:
- `ref()` para estado reactivo
- `computed()` para propiedades computadas
- Lifecycle hooks (`onBeforeMount`, `onMounted`, `onBeforeUnmount`)

### Props y Emits
- **Props**: Paso de datos de padre a hijo con validación
- **Emits**: Comunicación de hijo a padre mediante eventos personalizados

### Slots
- Uso de slots para contenido personalizable en las tarjetas de productos
- Permite agregar etiquetas especiales (ofertas, recomendaciones)

### Componentes Dinámicos
- Uso de `<component :is="componenteActivo">` para renderizado condicional
- Gestión eficiente de la vista de detalle

### Estilos Scoped
- Estilos encapsulados por componente
- Sin conflictos entre componentes
- CSS moderno con gradientes y animaciones

## 📱 Responsive Design

La aplicación es completamente responsive con breakpoints para:
- **Desktop**: Grid de múltiples columnas
- **Tablet**: Grid adaptativo
- **Mobile**: Vista de una columna con diseño vertical

## 🎯 Productos Incluidos

1. **Laptop HP Pavilion** - $899,990
2. **Mouse Inalámbrico** - $29,990
3. **Teclado Mecánico RGB** - $79,990 (Agotado)
4. **Monitor 27" 4K** - $449,990 (15% OFF)
5. **Auriculares Bluetooth** - $129,990
6. **Webcam Full HD** - $59,990 (Recomendado)

## 🐛 Debugging

El proyecto incluye mensajes en consola para seguimiento:
- Lifecycle hooks de componentes
- Eventos de carrito (agregar, vaciar)
- Estados de componentes

Abre las DevTools del navegador (F12) para ver estos mensajes.

## 📝 Conceptos Vue 3 Demostrados

✅ **Composition API** con `<script setup>`  
✅ **Reactividad** con `ref()` y `computed()`  
✅ **Props** con validación de tipos  
✅ **Custom Events** con `defineEmits()`  
✅ **Slots** para contenido personalizable  
✅ **Lifecycle Hooks** (beforeMount, mounted, beforeUnmount)  
✅ **Componentes Dinámicos** con `:is`  
✅ **v-for** para renderizado de listas  
✅ **v-if/v-else** para renderizado condicional  
✅ **Event Handling** con `@click`, `@click.self`  
✅ **Two-way Data Binding** implícito  
✅ **Scoped Styles** para encapsulación de CSS  

## 🤝 Contribución

Este es un proyecto educativo. Siéntete libre de:
- Hacer fork del repositorio
- Crear issues para reportar bugs
- Enviar pull requests con mejoras

## 📄 Licencia

Este proyecto es de código abierto y está disponible bajo la licencia MIT.

## 👨‍💻 Autor

<h4 align="center"> 
  <a href="https://github.com/CaroHernz">Carolina Hernández</a> | 
	<a href="https://github.com/gurrutia15">Gonzalo Urrutia</a> | 
	<a href="https://github.com/jlmansilla">Juan Luis Mansilla</a> | 
	<a href="https://github.com/lcarrilloq">Luis Carrillo</a> | 
</h4>


Desarrollado como parte del Módulo 7 - Bootcamp Desarrollo de Aplicaciones Front-end Trainee

---

⭐ Si te ha gustado este proyecto, no olvides darle una estrella en GitHub!
