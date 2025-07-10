<template>
  <div class="bg-black text-green-400 min-h-screen p-4">
    <div ref="terminal" class="whitespace-pre-wrap mb-4 h-[80vh] overflow-y-auto">
      <BootAnimation v-if="isBooting" @boot-finished="onBootFinished" />
      <template v-else>
        <template v-for="(line, index) in terminalLines" :key="index">
          {{ line }}<br />
        </template>
      </template>
    </div>

    <form v-if="!isBooting" @submit.prevent="handleCommand" class="flex items-center">
      <span class="text-green-400 mr-2">&gt;</span>
      <input
        v-model="command"
        type="text"
        class="bg-black text-green-400 w-full outline-none"
        autocomplete="off"
        autofocus
      />
    </form>
  </div>
</template>

<script setup>
import { ref, nextTick } from 'vue'

const terminal = ref(null)
const terminalLines = ref([])
const command = ref('')
const isBooting = ref(true)

function onBootFinished() {
  const asciiArt = `
  _____   ______ _     _ _     _ ______
 |     | |  ____ |_____| |     | |_____]
 |_____| |_____| |     | |_____| |_____]
  `
  terminalLines.value.push('>> CONECTADO')
  terminalLines.value.push(asciiArt)
  terminalLines.value.push('\nDigite "help" para ver os comandos disponíveis.')
  isBooting.value = false
  nextTick(() => {
    terminal.value.scrollTop = terminal.value.scrollHeight
  })
}

const commands = {
  help: `\nComandos disponíveis:\n  help        - mostra esta mensagem\n  inbox       - lista mensagens\n  decrypt 001 - descriptografa o arquivo 001\n  clear       - limpa o terminal`,
  inbox: `\n[📥] Mensagens disponíveis:\n - [001] Sombra Anônima: "Infiltrar Zentech - coordenadas anexadas"\n - [002] IA.007: "Seu IP foi rastreado, execute evasão imediatamente"`,
  'decrypt 001': `\nDescriptografando arquivo 001...\n███▓▒░ CONTEÚDO: [COORDENADAS: LAT-128.34, LON-21.56] ░▒▓███\nObjetivo: invadir a antena de transmissão subterrânea.`,
  clear: ''
}

function writeOutput(text) {
  terminalLines.value.push(text)
  nextTick(() => {
    terminal.value.scrollTop = terminal.value.scrollHeight
  })
}

function handleCommand() {
  const cmd = command.value.trim()
  writeOutput(`> ${cmd}`)
  const response = commands[cmd.toLowerCase()] || '[ERRO] Comando não reconhecido.'
  if (cmd.toLowerCase() === 'clear') {
    terminalLines.value = []
  } else {
    writeOutput(response)
  }
  command.value = ''
}
</script>
