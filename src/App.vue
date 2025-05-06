<script setup lang="ts">
import {onMounted, ref} from "vue";

interface Data {
  CounterMain: number
  CounterStudentRules: number
  CounterLyceumRegulation: number
  CounterResponsibleInfo: number
  CounterLicenseRegistry: number
  CounterAccreditation: number
  CounterEducationLicense: number
  CounterCharterChanges: number
  CounterEGRUL: number
  CounterEducationActivityLicense: number
  CounterAccreditationAppendix: number
}

const data = ref<Data | null>(null)
const baseUrl = "https://formulink.duckdns.org/lyceum-6/"

onMounted(async () => {
  try {
    const resp = await fetch("https://formulink.duckdns.org/counters")
    data.value = await resp.json()
  } catch (e) {
    console.error(e)
  }
})

const cards: {
  title: string;
  counterKey: keyof Data;
  yourUrl: string;
  url: string;
  qr: string;
}[] = [
  {
    title: 'Главная страница',
    counterKey: 'CounterMain',
    yourUrl: `${baseUrl}main`,
    url: 'https://licey-6.odinedu.ru',
    qr: 'main'
  },
  {
    title: 'Правила распорядка обучения',
    counterKey: 'CounterStudentRules',
    yourUrl: `${baseUrl}student-rules`,
    url: 'https://licey-6.odinedu.ru/2024/02/15/%D0%BF%D1%80%D0%B0%D0%B2%D0%B8%D0%BB%D0%B0-%D0%B2%D0%BD%D1%83%D1%82%D1%80%D0%B5%D0%BD%D0%BD%D0%B5%D0%B3%D0%BE-%D1%80%D0%B0%D1%81%D0%BF%D0%BE%D1%80%D1%8F%D0%B4%D0%BA%D0%B0-%D0%BE%D0%B1%D1%83%D1%87//',
    qr: 'student-rules'
  },
  {
    title: 'Устав лицея',
    counterKey: 'CounterLyceumRegulation',
    yourUrl: `${baseUrl}lyceum-regulation`,
    url: 'https://licey-6.odinedu.ru/2023/08/15/%D1%83%D1%81%D1%82%D0%B0%D0%B2-%D0%BC%D0%B0%D0%BE%D1%83-%D0%BE%D0%B4%D0%B8%D0%BD%D1%86%D0%BE%D0%B2%D1%81%D0%BA%D0%BE%D0%B3%D0%BE-%D0%BB%D0%B8%D1%86%D0%B5%D1%8F-%E2%84%966-%D0%B8%D0%BC-%D0%B0-%D1%81/',
    qr: 'lyceum-regulation'
  },
  {
    title: 'Сведения об ответственных',
    counterKey: 'CounterResponsibleInfo',
    yourUrl: `${baseUrl}responsible-info`,
    url: 'https://licey-6.odinedu.ru/2024/02/15/сведения-об-ответственных-лиц/',
    qr: 'responsible-info'
  },
  {
    title: 'Реестр лицензий',
    counterKey: 'CounterLicenseRegistry',
    yourUrl: `${baseUrl}license-registry`,
    url: 'https://licey-6.odinedu.ru/2024/02/15/реестр-лицензий/',
    qr: 'license-registry'
  },
  {
    title: 'Свидетельство о гос. аккредитации',
    counterKey: 'CounterAccreditation',
    yourUrl: `${baseUrl}accreditation`,
    url: 'https://licey-6.odinedu.ru/2024/02/15/свидетельство-о-государственной-акк/',
    qr: 'accreditation'
  },
  {
    title: 'Лицензия на образовательную деятельность',
    counterKey: 'CounterEducationLicense',
    yourUrl: `${baseUrl}education-license`,
    url: 'https://licey-6.odinedu.ru/2024/02/15/лицензия-на-образовательную-деятельн/',
    qr: 'education-license'
  },
  {
    title: 'Изменения в уставе',
    counterKey: 'CounterCharterChanges',
    yourUrl: `${baseUrl}charter-changes`,
    url: 'https://licey-6.odinedu.ru/2024/02/15/изменения-в-уставе/',
    qr: 'charter-changes'
  },
  {
    title: 'Выписка из ЕГРЮЛ',
    counterKey: 'CounterEGRUL',
    yourUrl: `${baseUrl}egrul`,
    url: 'https://licey-6.odinedu.ru/2024/02/15/выписка-из-егрюл/',
    qr: 'egrul'
  },
  {
    title: 'Лицензия на образовательную деятельность (продолжение)',
    counterKey: 'CounterEducationActivityLicense',
    yourUrl: `${baseUrl}education-activity-license`,
    url: 'https://licey-6.odinedu.ru/2024/09/02/лицензия-на-образовательную-деятельн-2/',
    qr: 'education-activity-license'
  },
  {
    title: 'Свидетельство о гос. аккредитации (Приложение)',
    counterKey: 'CounterAccreditationAppendix',
    yourUrl: `${baseUrl}accreditation-appendix`,
    url: 'https://licey-6.odinedu.ru/2024/09/02/свидетельство-о-государственной-акк-4/',
    qr: 'accreditation-appendix'
  }
]


</script>
<template>
  <div v-if="data" class="app">
    <div class="main-container">
      <div
          class="card"
          v-for="(item, index) in cards"
          :key="index"
      >
        <div class="card-content">
          <h2>{{ item.title }}</h2>
          <div class="counter">{{ data[item.counterKey] }} переходов</div>
          <span class="your-url">{{ item.yourUrl }}<br /></span>
          <span class="url">{{ item.url }}</span>
        </div>
        <div class="qr-code">
          <a href="http://qrcoder.ru" target="_blank">
            <img
                :src="`http://qrcoder.ru/code/?https%3A%2F%2Fformulink.duckdns.org%2Flyceum-6%2F${item.qr}&4&0`"
                :alt="`${item.title} QR`"
                width="164"
                height="164"
                title="QR код"
            />
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
  padding-bottom: 20px;
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