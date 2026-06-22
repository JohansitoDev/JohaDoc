<template>
  <div v-if="doc" class="glass-card rounded-2xl p-6 md:p-8 min-h-[60vh] shadow-xl relative transition-all duration-300">
    <div class="flex justify-between items-start border-b border-slate-500/20 pb-4 mb-6">
      <div>
        <span :class="['text-xs font-mono font-bold uppercase tracking-widest px-2 py-0.5 rounded', theme === 'black' ? 'bg-cyan-500/10 border border-cyan-500/20 text-cyan-400' : 'bg-sky-500/10 border border-sky-500/20 text-sky-400']">
          {{ doc.categoria || 'General' }}
        </span>
        <h1 class="text-2xl md:text-3xl font-bold text-white tracking-tight mt-2">{{ doc.titulo }}</h1>
        <p class="text-[11px] text-slate-500 font-mono mt-1">Modificado: {{ doc.fecha }}</p>
      </div>
      <div class="flex space-x-2">
        <button @click="$emit('edit-doc', doc.id)" class="p-2 bg-slate-800/20 border border-slate-500/30 hover:border-cyan-500 text-slate-400 hover:text-cyan-500 rounded-lg transition-all" title="Editar">
          <svg class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15.232 5.232l3.536 3.536m-2.036-5.036a2.5 2.5 0 113.536 3.536L6.5 21.036H3v-3.572L16.732 3.732z" /></svg>
        </button>
        <button @click="$emit('delete-doc', doc.id)" class="p-2 bg-red-950/10 border border-red-500/20 hover:border-red-500 text-red-400 rounded-lg transition-all" title="Eliminar">
          <svg class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-16v1a3 3 0 003 3h10M4 7h16" /></svg>
        </button>
      </div>
    </div>
    <div 
      class="prose max-w-none font-mono text-sm leading-relaxed p-4 rounded-xl border bg-slate-950/40 border-slate-800/60 text-slate-300"
      v-html="contenidoFormateado"
    ></div>
  </div>
  
  <div v-else class="glass-card rounded-2xl p-8 min-h-[60vh] flex flex-col items-center justify-center text-center transition-all duration-300">
    <div class="h-16 w-16 bg-slate-800/20 rounded-full flex items-center justify-center mb-4 border border-slate-700/40">
      <svg class="h-8 w-8 text-slate-400" fill="none" viewBox="0 0 24 24" stroke="currentColor">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M12 6.253v13m0-13C10.832 5.477 9.246 5 7.5 5S4.168 5.477 3 6.253v13C4.168 18.477 5.754 18 7.5 18s3.332.477 4.5 1.253m0-13C13.168 5.477 14.754 5 16.5 5c1.747 0 3.332.477 4.5 1.253v13C19.832 18.477 18.247 18 16.5 18c-1.746 0-3.332.477-4.5 1.253" />
      </svg>
    </div>
    <h3 class="text-lg font-medium text-slate-400">Ningún documento seleccionado</h3>
    <p class="text-slate-500 text-sm mt-1 max-w-sm">Selecciona un artículo del menú lateral o empieza creando uno nuevo desde el botón superior.</p>
  </div>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
  doc: Object,
  theme: String
});

defineEmits(['edit-doc', 'delete-doc']);

const contenidoFormateado = computed(() => {
  if (!props.doc) return '';
  return props.doc.contenido
    .replace(/&/g, "&amp;")
    .replace(/</g, "&lt;")
    .replace(/>/g, "&gt;")
    .replace(/\n/g, "<br>");
});
</script>