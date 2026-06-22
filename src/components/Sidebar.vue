<template>
  <aside class="space-y-4">
    <div>
      <h2 class="text-xs font-semibold text-slate-500 uppercase tracking-wider px-2 mb-2">Buscar artículo</h2>
      <input 
        v-model="filtro" 
        type="text" 
        placeholder="Filtrar por título o tag..." 
        class="w-full bg-slate-950/60 border border-slate-800/80 rounded-lg px-3 py-2 text-sm focus:outline-none focus:border-cyan-500 focus:ring-1 focus:ring-cyan-500 transition-all text-slate-200 placeholder-slate-500"
      >
    </div>

    <h2 class="text-xs font-semibold text-slate-500 uppercase tracking-wider px-2 pt-2">Artículos</h2>
    <div class="space-y-1 max-h-[60vh] overflow-y-auto pr-2">
      <p v-if="docsFiltrados.length === 0" class="text-xs text-slate-500 px-2 italic">
        No se encontraron artículos.
      </p>
      
      <button 
        v-for="doc in docsFiltrados" 
        :key="doc.id"
        @click="$emit('select-doc', doc.id)"
        :class="[
          'w-full text-left px-3 py-2.5 rounded-lg text-sm transition-all flex flex-col space-y-0.5 group',
          doc.id === activeId 
            ? (theme === 'black' ? 'bg-gradient-to-r from-cyan-950/40 to-slate-900 border-l-2 border-cyan-500 text-cyan-400' : 'bg-gradient-to-r from-cyan-950/60 to-slate-900/60 border-l-2 border-sky-400 text-sky-300 font-medium')
            : 'text-slate-400 hover:bg-slate-900/40 hover:text-slate-200'
        ]"
      >
        <span class="truncate text-slate-200 group-hover:text-white font-medium">{{ doc.titulo }}</span>
        <span :class="['text-[10px] font-mono uppercase tracking-wide', doc.id === activeId ? (theme === 'black' ? 'text-cyan-500' : 'text-sky-400') : 'text-slate-500']">
          {{ doc.categoria || 'General' }}
        </span>
      </button>
    </div>
  </aside>
</template>

<script setup>
import { ref, computed } from 'vue';

const props = defineProps({
  documentos: Array,
  activeId: String,
  theme: String
});

defineEmits(['select-doc']);

const filtro = ref('');

const docsFiltrados = computed(() => {
  const query = filtro.value.toLowerCase();
  return props.documentos.filter(doc => 
    doc.titulo.toLowerCase().includes(query) || 
    (doc.categoria && doc.categoria.toLowerCase().includes(query))
  );
});
</script>