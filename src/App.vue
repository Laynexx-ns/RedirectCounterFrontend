<script setup lang="ts">
import {onMounted, ref} from "vue";

interface Data{
  CounterMain: number,
  CounterStudentRules: number,
  CounterLyceumRegulation: number,
}
const data = ref<Data | null>(null);

onMounted(async ()=>{
  try{
    const resp = await fetch("https://arthur-izmailyan.duckdns.org/counters")
    data.value = await resp.json()
    console.log(data.value)
  } catch(e){
    console.log(e)
  }
})
</script>

<template>
  <div v-if="data" class="app">
    <div class="main-container">
      <div class="card">
        <div class="card-content">
          <h2>Главная страница</h2>
          <div class="counter">{{ data.CounterMain }}</div>
          <span class="your-url">https://arthur-izmailyan.duckdns.org/lyceum-6/main <br/></span>
          <span class="url">https://licey-6.odinedu.ru</span>
        </div>
        <div class="qr-code">
          <a href="http://qrcoder.ru" target="_blank">
            <img src="/qr1.png" alt="main qr" title="QR код">
          </a>
        </div>
      </div>

      <div class="card">
        <div class="card-content">
          <h2>Правила распорядка обучения</h2>
          <div class="counter">{{ data.CounterStudentRules }}</div>
          <span class="your-url">https://arthur-izmailyan.duckdns.org/lyceum-6/student-rules <br/></span>
          <span class="url">https://licey-6.odinedu.ru/2024/02/15/правила-внутреннего-распорядка-обуч/</span>
        </div>
        <div class="qr-code">
          <a href="http://qrcoder.ru" target="_blank">
            <img src="/qr2.png" alt="main qr" title="QR код">
          </a>
        </div>
      </div>

      <div class="card">
        <div class="card-content">
          <h2>Устав лицея</h2>
          <div class="counter">{{ data.CounterLyceumRegulation }}</div>
          <span class="your-url">https://arthur-izmailyan.duckdns.org/lyceum-6/lyceum-regulation <br/></span>
          <span class="url">https://licey-6.odinedu.ru/2023/08/15/устав-маоу-одинцовского-лицея-№6-им-а-с/</span>
        </div>
        <div class="qr-code">
          <a href="http://qrcoder.ru" target="_blank">
            <img src="/qr3.png" alt="main qr" title="QR код">
          </a>
        </div>
      </div>
    </div>
  </div>
</template>

<style>
:root {
  --bg-color: #121212;
  --card-bg: #1e1e1e;
  --card-border: #333333;
  --text-primary: #e0e0e0;
  --text-secondary: #a0a0a0;
  --accent: #bb86fc;
  --accent-secondary: #03dac6;
}

body {
  margin: 0;
  padding: 0;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
  background-color: var(--bg-color);
  color: var(--text-primary);
}

.app {
  min-height: 100vh;
  padding: 1rem;
  background-color: var(--bg-color);
}

.main-container {
  max-width: 1200px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
  padding: 1rem 0;
}

.card {
  background: var(--card-bg);
  border-radius: 12px;
  overflow: hidden;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.4);
  border: 1px solid var(--card-border);
  display: flex;
  flex-direction: column;
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.card:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 25px rgba(0, 0, 0, 0.5);
}

.card-content {
  padding: 1.5rem;
  flex: 1;
}

h2 {
  margin: 0 0 0.75rem 0;
  font-size: 1.25rem;
  font-weight: 600;
  color: var(--text-primary);
}

.counter {
  font-size: 3rem;
  font-weight: 700;
  color: var(--accent);
  margin-bottom: 0.5rem;
  text-shadow: 0 0 10px rgba(187, 134, 252, 0.3);
}

.url {
  font-size: 0.875rem;
  color: var(--text-secondary);
}

.qr-code {
  background: #2d2d2d;
  padding: 1rem;
  display: flex;
  justify-content: center;
  align-items: center;
  border-top: 1px solid var(--card-border);
}

.qr-code img {
  max-width: 100%;
  height: auto;
  display: block;
  border-radius: 8px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);
}

/* Mobile responsive styles */
@media (min-width: 640px) {
  .card {
    flex-direction: row;
    align-items: center;
  }

  .card-content {
    padding: 2rem;
  }

  .qr-code {
    flex: 0 0 auto;
    padding: 1.5rem;
    border-top: none;
    border-left: 1px solid var(--card-border);
  }

  .qr-code img {
    width: 120px;
    height: 120px;
  }
}

@media (max-width: 639px) {
  .card-content {
    text-align: center;
  }

  .counter {
    font-size: 2rem;
  }

  .qr-code img {
    width: 140px;
    height: 140px;
    margin: 0 auto;
  }
}

@media (max-width: 380px) {
  .card-content {
    padding: 1rem;
  }

  h2 {
    font-size: 1.1rem;
  }

  .counter {
    font-size: 1.75rem;
  }

  .qr-code {
    padding: 0.75rem;
  }

  .qr-code img {
    width: 120px;
    height: 120px;
  }
}
</style>