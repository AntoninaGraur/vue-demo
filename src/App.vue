<script setup>
import { ref, computed } from 'vue'

const count = ref(0)
const renderCount = ref(0)
const lastAction = ref('Noch kein Klick')

const label = computed(() => 'Anzahl: ' + count.value)

function increment() {
  count.value++
  renderCount.value++
  lastAction.value = 'count++ → neuer Wert: ' + count.value
}

function reset() {
  count.value = 0
  renderCount.value++
  lastAction.value = 'count zurückgesetzt → 0'
}
</script>

<template>
  <main class="page">

    <header>
      <h1>Vue-Reaktivität</h1>

      <p class="subtitle">


      </p>
    </header>

    <section class="flow">

      <article class="card state" :class="{ active: lastAction !== 'Noch kein Klick' }">
        <h2>Zustand</h2>

        <div class="value">
          count = {{ count }}
        </div>

        <small>Reaktiver Zustand</small>
      </article>

      <div class="arrow">›</div>

      <article class="card react" :class="{ active: lastAction !== 'Noch kein Klick' }">
        <h2>Vue reagiert</h2>

        <div class="value">
          Abhängigkeit erkannt
        </div>

        <small>
          Vue erkennt die Änderung von count
        </small>
      </article>

      <div class="arrow">›</div>

      <article class="card ui" :class="{ active: lastAction !== 'Noch kein Klick' }">
        <h2>Oberfläche</h2>

        <div class="value">
          „{{ label }}“
        </div>

        <small>
          Die Anzeige wird automatisch aktualisiert
        </small>
      </article>

    </section>

    <section class="controls">
      <button @click="increment">
        Klick
      </button>

      <button class="secondary" @click="reset">
        Zurücksetzen
      </button>
    </section>

    <section class="live">
      <span class="dot"></span>
      <p>
        {{ lastAction }}
      </p>

      <p class="hint">

        Aktualisierungen:
        <b>{{ renderCount }}</b>
      </p>
    </section>



  </main>
</template>

<style>
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  background: #07101a;
  color: #eef5ff;
  font-family: Arial, system-ui, sans-serif;
}

.page {
  max-width: 1100px;
  margin: auto;
  padding: 42px 24px 60px;
}

header {
  text-align: center;
  margin-bottom: 35px;
}

h1 {
  color: #42b883;
  font-size: 42px;
  margin: 0 0 100px;
}

.subtitle {
  color: #a9bdd2;
  font-size: 18px;
}

.flow {
  display: grid;
  grid-template-columns: 1fr auto 1fr auto 1fr;
  gap: 18px;
  align-items: center;
}

.card {
  min-height: 220px;
  padding: 28px;
  border: 3px solid;
  border-radius: 14px;
  background: #102a43;
  display: flex;
  flex-direction: column;
  justify-content: center;
  transition: 0.2s;
}

.state {
  border-color: #3194df;
}

.react {
  border-color: #42b883;
}

.ui {
  border-color: #16c7c7;
}

.card.active {
  transform: translateY(-6px);
  box-shadow: 0 0 30px #42b88366;
}

h2 {
  color: #16c7c7;
  text-align: center;
  font-size: 28px;
  margin: 0 0 28px;
}

.value {
  text-align: center;
  font-size: 23px;
  color: #c2d3e5;
}

small {
  text-align: center;
  color: #829bb5;
  margin-top: 20px;
}

.arrow {
  font-size: 70px;
  color: #42b883;
}

.controls {
  text-align: center;
  margin: 34px 0 22px;
}

button {
  border: 0;
  border-radius: 10px;
  padding: 14px 25px;
  width: 150px;
  margin: 5px;
  font-size: 17px;
  font-weight: bold;
  cursor: pointer;
  color: white;
  background: #42b883;
}

button.secondary {
  background: #29445e;
}

.live,
.explain {
  max-width: 760px;
  margin: 20px auto;
  padding: 20px 24px;
  background: #0d2033;
  border: 1px solid #29445e;
  border-radius: 12px;
}

.dot {
  display: inline-block;
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background: #42b883;
  box-shadow: 0 0 12px #42b883;
  margin-right: 8px;
}

.live p {
  color: #c6d7e8;
}

.hint {
  font-size: 14px;
  color: #8199b1 !important;
}

.explain {
  border-left: 4px solid #42b883;
  border-radius: 0;
  color: #b9ccdf;
  line-height: 1.6;
}

code {
  color: #75e0ae;
}

@media (max-width: 800px) {
  .flow {
    grid-template-columns: 1fr;
  }

  .arrow {
    text-align: center;
    transform: rotate(90deg);
    height: 50px;
  }

  .card {
    min-height: 170px;
  }
}
</style>