<template>
  <div class="bg-black min-h-screen flex items-center justify-center font-vt323">
    <form @submit.prevent="handleLogin" class="bg-black text-green-400 p-8 rounded shadow-lg w-full max-w-xs flex flex-col gap-6">
      <h1 class="text-3xl mb-6 text-center">LOGIN</h1>
      <div>
        <label for="username" class="block mb-1">Usuário</label>
        <div class="ascii-input mt-2">
          <input id="username" v-model="username" type="text" class="bg-black text-green-400 w-full outline-none px-1 py-0.5 font-vt323" autocomplete="off" />
        </div>
      </div>
      <div>
        <label for="password" class="block mb-1">Senha</label>
        <div class="ascii-input mt-2">
          <input id="password" v-model="password" type="password" class="bg-black text-green-400 w-full outline-none px-1 py-0.5 font-vt323" autocomplete="off" />
        </div>
      </div>
      <button type="submit" class="blink-btn mt-4 font-vt323 transition">Entrar</button>
    </form>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { useRouter } from 'vue-router'
const username = ref('')
const password = ref('')
const router = useRouter()

const handleLogin = () => {
  router.push('/')
}
</script>

<style scoped>
.ascii-input {
  position: relative;
  padding: 0;
  margin: 0;
}
.ascii-input input {
  border: none;
  outline: none;
  background: transparent;
  position: relative;
  z-index: 1;
}
.ascii-input::before {
  content: "+----------------------+";
  color: #22c55e;
  position: absolute;
  top: -1.2em;
  left: 0;
  font-family: 'VT323', monospace;
  font-size: 1.1em;
  pointer-events: none;
}
.ascii-input::after {
  content: "+----------------------+";
  color: #22c55e;
  position: absolute;
  bottom: -1.2em;
  left: 0;
  font-family: 'VT323', monospace;
  font-size: 1.1em;
  pointer-events: none;
}
.ascii-input {
  padding-top: 1.2em;
  padding-bottom: 1.2em;
}
.blink-btn {
  background: none;
  border: none;
  color: #22c55e;
  font-size: 1.2em;
  padding: 0.5em 0;
  cursor: pointer;
  outline: none;
  transition: none;
}
.blink-btn:hover, .blink-btn:focus {
  animation: blink 0.5s steps(2, start) 1;
}
@keyframes blink {
  0%   { background: none; color: #22c55e; }
  25%  { background: #000; color: #fff; }
  50%  { background: none; color: #22c55e; }
  75%  { background: #fff; color: #000; }
  100% { background: none; color: #22c55e; }
}
</style>