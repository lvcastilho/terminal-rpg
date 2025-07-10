<template>
  <div ref="bootRef" class="whitespace-pre-wrap text-green-400">
    <template v-for="(line, index) in bootLinesDisplay" :key="index">
      {{ line }}<br />
    </template>
  </div>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount, nextTick, defineEmits } from 'vue'

const emit = defineEmits(['boot-finished'])

const bootRef = ref(null)
const bootLinesDisplay = ref([])
const loadingDots = ref('')
let interval
let dotCount = 0

const maxDots = 3

const bootLines = [
  '>> ACESSANDO TERMINAL SEGURO',
  ':: Inicializando protocolo de evasão...',
  ':: Estabelecendo conexão com IA.007...',
  ':: Decodificando canais criptografados...',
  ':: Aguardando resposta do satélite Z3-9',
  ':: Sincronizando coordenadas subterrâneas',
  ':: Estabilizando shell quântico'
]

function addLineWithDelay(lines, delay = 500) {
  lines.forEach((line, index) => {
    setTimeout(() => {
      bootLinesDisplay.value.push(line)
    }, delay * index)
  })
}

onMounted(() => {
  interval = setInterval(() => {
    dotCount = (dotCount + 1) % (maxDots + 1)
    loadingDots.value = '.'.repeat(dotCount)
    const lastIndex = bootLinesDisplay.value.length - 1
    if (bootLinesDisplay.value[lastIndex]?.startsWith('>> ACESSANDO')) {
      bootLinesDisplay.value[lastIndex] = '>> ACESSANDO TERMINAL SEGURO' + loadingDots.value
    }
  }, 300)

  addLineWithDelay(bootLines)

  setTimeout(() => {
    clearInterval(interval)
    emit('boot-finished')
  }, bootLines.length * 500 + 1000)
})

onBeforeUnmount(() => {
  clearInterval(interval)
})
</script>

<style scoped>
div {
  font-family: 'VT323', monospace;
}
</style>
