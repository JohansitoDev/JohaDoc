<template>
  <div :class="['min-h-screen font-sans antialiased transition-colors duration-300', theme === 'blue' ? 'theme-blue bg-[#0a192f]' : 'theme-black bg-[#05070f]']">
    
    <Navbar @toggle-theme="alternarTema" @open-create="abrirModalCrear" />

    <div class="max-w-7xl mx-auto px-4 py-8 grid grid-cols-1 md:grid-cols-4 gap-6">
      <Sidebar 
        :documentos="documentos" 
        :activeId="idDocumentoActivo" 
        :theme="theme"
        @select-doc="idDocumentoActivo = $event" 
      />
      
      <main class="md:col-span-3">
        <DocViewer 
          :doc="docSeleccionado" 
          :theme="theme"
          @edit-doc="abrirModalEditar" 
          @delete-doc="eliminarDocumento" 
        />
      </main>
    </div>

    <div v-if="modalAbierto" class="fixed inset-0 z-50 bg-black/60 backdrop-blur-sm flex items-center justify-center p-4">
      <div class="glass-card w-full max-w-2xl rounded-2xl shadow-2xl overflow-hidden p-6 space-y-4">
        <div class="flex justify-between items-center border-b border-slate-800/40 pb-2">
          <h3 class="text-lg font-semibold text-slate-200">{{ form.id ? 'Actualizar Documentación' : 'Nueva Documentación' }}</h3>
          <button @click="modalAbierto = false" class="text-slate-400 hover:text-slate-200">
            <svg class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" /></svg>
          </button>
        </div>
        <form @submit.prevent="guardarDocumento" class="space-y-4">
          <div>
            <label class="block text-xs font-medium text-slate-400 uppercase tracking-wider mb-1">Título</label>
            <input v-model="form.titulo" type="text" required class="w-full bg-slate-900/40 border border-slate-700/50 rounded-lg px-4 py-2.5 text-slate-200 text-sm focus:outline-none focus:border-cyan-500">
          </div>
          <div>
            <label class="block text-xs font-medium text-slate-400 uppercase tracking-wider mb-1">Categoría / Tag</label>
            <input v-model="form.categoria" type="text" placeholder="Ej: Frontend, Backend" class="w-full bg-slate-900/40 border border-slate-700/50 rounded-lg px-4 py-2.5 text-slate-200 text-sm focus:outline-none focus:border-cyan-500">
          </div>
          <div>
            <label class="block text-xs font-medium text-slate-400 uppercase tracking-wider mb-1">Contenido</label>
            <textarea v-model="form.contenido" required rows="10" class="w-full bg-slate-900/40 border border-slate-700/50 rounded-lg px-4 py-2.5 text-slate-200 text-sm font-mono focus:outline-none focus:border-cyan-500"></textarea>
          </div>
          <div class="flex justify-end space-x-3 pt-2">
            <button type="button" @click="modalAbierto = false" class="px-4 py-2 rounded-lg bg-slate-800/40 text-slate-300 text-sm hover:bg-slate-700">Cancelar</button>
            <button type="submit" class="px-4 py-2 rounded-lg bg-gradient-to-r from-cyan-500 to-blue-500 text-white text-sm font-medium">Guardar Documento</button>
          </div>
        </form>
      </div>
    </div>

  </div>
</template>

<script setup>
import { ref, computed, watch } from 'vue';
import Navbar from './components/Navbar.vue';
import Sidebar from './components/Sidebar.vue';
import DocViewer from './components/DocViewer.vue';

const documentos = ref(JSON.parse(localStorage.getItem('joha_docs')) || []);
const idDocumentoActivo = ref(null);
const theme = ref(localStorage.getItem('joha_theme') || 'black');
const modalAbierto = ref(false);

const form = ref({ id: '', titulo: '', categoria: '', contenido: '' });

const docSeleccionado = computed(() => documentos.value.find(d => d.id === idDocumentoActivo.value));

watch(documentos, (nuevosDocs) => {
  localStorage.setItem('joha_docs', JSON.stringify(nuevosDocs));
}, { deep: true });

const alternarTema = () => {
  theme.value = theme.value === 'black' ? 'blue' : 'black';
  localStorage.setItem('joha_theme', theme.value);
};

const abrirModalCrear = () => {
  form.value = { id: '', titulo: '', categoria: '', contenido: '' };
  modalAbierto.value = true;
};

const abrirModalEditar = (id) => {
  const doc = documentos.value.find(d => d.id === id);
  if (doc) {
    form.value = { ...doc };
    modalAbierto.value = true;
  }
};

const guardarDocumento = () => {
  const fechaActual = new Date().toLocaleString();
  if (form.value.id) {
    documentos.value = documentos.value.map(d => d.id === form.value.id ? { ...form.value, fecha: fechaActual } : d);
  } else {
    const nuevo = { ...form.value, id: 'doc_' + Date.now(), fecha: fechaActual };
    documentos.value.push(nuevo);
    idDocumentoActivo.value = nuevo.id;
  }
  modalAbierto.value = false;
};

const eliminarDocumento = (id) => {
  if (confirm('¿Seguro que deseas eliminar esta documentación?')) {
    documentos.value = documentos.value.filter(d => d.id !== id);
    if (idDocumentoActivo.value === id) idDocumentoActivo.value = null;
  }
};
</script>

<style>

.theme-black .glass-card { background: rgba(13, 17, 30, 0.7); border: 1px solid rgba(255, 255, 255, 0.04); backdrop-filter: blur(12px); }
.theme-black .glass-nav { background: rgba(13, 17, 30, 0.8); border-bottom: 1px solid #111726; backdrop-filter: blur(12px); }

.theme-blue .glass-card { background: rgba(16, 29, 54, 0.6); border: 1px solid rgba(56, 189, 248, 0.1); backdrop-filter: blur(12px); }
.theme-blue .glass-nav { background: rgba(16, 29, 54, 0.8); border-bottom: 1px solid rgba(56, 189, 248, 0.15); backdrop-filter: blur(12px); }
</style>