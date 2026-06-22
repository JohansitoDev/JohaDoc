<template>
  <header class="glass-nav sticky top-0 z-50 px-6 py-4 flex justify-between items-center transition-all duration-300">
    <div class="flex items-center space-x-3">
      <div class="h-8 w-8 bg-gradient-to-tr from-cyan-500 to-blue-600 rounded-lg flex items-center justify-center font-bold text-white shadow-lg shadow-cyan-500/20">J</div>
      <span class="text-xl font-bold tracking-tight text-white">JohaDocs</span>
    </div>
    
    <div class="flex items-center space-x-4">
      <button 
        @click="$emit('toggle-theme')" 
        class="p-2 rounded-lg bg-slate-800/40 border border-slate-700/50 hover:bg-slate-700/80 transition-all text-cyan-400"
        title="Cambiar Combinación de Fondo"
      >
        <svg class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M7 21a4 4 0 01-4-4V5a2 2 0 012-2h4a2 2 0 012 2v12a4 4 0 01-4 4zm0 0h12a2 2 0 002-2v-4a2 2 0 00-2-2h-2.343M11 7.344l5.707-5.707a1 1 0 011.414 0l1.414 1.414a1 1 0 010 1.414L13.828 10.25M4.5 16.5H4.51" />
        </svg>
      </button>

      <button 
        @click="$emit('open-create')" 
        class="bg-gradient-to-r from-cyan-500 to-blue-500 hover:from-cyan-600 hover:to-blue-600 text-white font-medium px-4 py-2 rounded-lg transition-all transform hover:scale-[1.02] shadow-lg shadow-cyan-500/10 text-sm"
      >
        + Nueva Documentación
      </button>
    </div>
  </header>
</template>

<script setup>
defineEmits(['toggle-theme', 'open-create']);
</script>