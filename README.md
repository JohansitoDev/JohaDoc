# JohaDocs PRO (Vue 3 Edition) 🚀

**JohaDocs PRO** es mi base de conocimientos y sistema de documentación técnico personal, rediseñado completamente sobre **Vue 3 (Composition API)** y estilizado con **Tailwind CSS**. Esta evolución toma el concepto original y lo transforma en una aplicación modular de nivel profesional, optimizada para centralizar apuntes tecnológicos, *playbooks* de ciberseguridad, configuraciones de red y fragmentos de código de manera rápida, fluida y privada.

La aplicación es completamente autónoma y respeta la privacidad de los datos al utilizar persistencia local absoluta.

---

## 🏗️ Arquitectura Modular (3 Componentes)

Para garantizar un código limpio, escalable y mantenible basado en un flujo unidireccional de datos, dividí la aplicación en tres componentes estratégicos orquestados por un nodo central:

1. **`Navbar.vue` (Encabezado de Control):** Maneja la identidad visual, el disparador de creación de nuevos artículos y el switch interactivo para alternar los entornos de visualización.
2. **`Sidebar.vue` (Índice y Filtrado Reactivo):** Incorpora un buscador síncrono que filtra instantáneamente los documentos por título o etiquetas (*tags*) mediante propiedades computadas de Vue.
3. **`DocViewer.vue` (Renderizador Seguro):** Centraliza la visualización de las notas, aplica filtros de sanitización para prevenir inyecciones de código y expone los disparadores para mutación (edición) y borrado.
4. **`App.vue` (Orquestador Global):** Actúa como la única fuente de verdad ($Source$ $of$ $Truth$), gestionando el estado reactivo global y sincronizando los cambios en segundo plano con el navegador.

---

## ✨ Características Implementadas

* **Persistencia Local Automática:** Implementé un *watcher* profundo (`{ deep: true }`) en Vue que monitorea el estado de mis notas y las guarda atómicamente en el `localStorage`. Los datos jamás viajan a servidores externos.
* **Entornos Oscuros Personalizados:** Eliminé los esquemas claros para mantener una estética puramente hacker/tecnológica. El switch alterna entre dos configuraciones cómodas para largas sesiones de lectura:
  * **Modo Cyberpunk:** Fondo negro puro (`#05070f`) con acentos cian y contrastes limpios.
  * **Modo Deep Blue:** Fondo azul marino de alta tecnología (`#0a192f`) con detalles en azul cielo.
* **Buscador en Tiempo Real:** Filtrado predictivo instantáneo que busca coincidencias tanto en los títulos como en las categorías asignadas.
* **Operaciones CRUD Completas:** Interfaz fluida y limpia para Crear, Leer, Actualizar y Eliminar registros mediante ventanas modales integradas.

---

## 🛠️ Tecnologías Utilizadas

* **Vue 3** (Sintaxis moderna con `<script setup>`)
* **Tailwind CSS** (Diseño interactivo, utilidades y efectos *glassmorphism*)
* **LocalStorage API** (Base de datos local en el navegador)
* **JavaScript Moderno (ES6+)**

---

## 🚀 Instalación y Uso

Para correr este proyecto en mi entorno de desarrollo local, sigo estos pasos:

1. **Clonar el repositorio:**
   ```bash
   git clone [https://github.com/JohansitoDev/johadocs-vue.git](https://github.com/tu-usuario/johadocs-vue.git)
   cd johadocs-vue