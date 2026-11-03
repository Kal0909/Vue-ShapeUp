<!--<script setup>
import { ref } from 'vue'

const name = ref('Kalel O'Gorman')
const bio = ref('Hit me, Batman!')
const likes = ref(0)
const showFact = ref(false)
const fact = ref('Fun fact this is my fact..')
const hobbies = ref(['Snowboarding','Dying hair','Eating popcorn'])
// TASK 4: Create a reactive likes counter.
// TASK 5: Create reactive showFact and fact values.
</script>-->

<!--
<template>
  <main>
    <article class="card">
      <p class="eyebrow">MY FIRST VUE PAGE</p>
      <h1>{{ name }}</h1>
      <p>{{ bio }}</p>
      &lt;!&ndash; TASK 2: Add a labelled input with v-model="name" here. &ndash;&gt;
      <label for="name">Your name</label>
      <input id="name" v-model="name" maxlength="60">
      <label for="bio">Your bio</label>
      <input id="bio" v-model="bio" maxlength="60">
      &lt;!&ndash; TASK 4: Add a button, click counter and @click here. &ndash;&gt;
      <button type="button" @click="likes++">Like this page</button>
      <button type="button" @click="likes = 0">Reset counter</button>
      <p aria-live="polite">Likes: {{ likes }}</p>
      &lt;!&ndash; TASK 5: Add a toggle button and v-if paragraph here. &ndash;&gt;
      <button type="button" @click="showFact = !showFact"
              :aria-expanded="showFact" aria-controls="fact">
        {{ showFact ? 'Hide fun fact' : 'Show fun fact' }}
      </button>
      <p id="fact" v-if="showFact">{{ fact }}</p>
      &lt;!&ndash; Optional challenges &ndash;&gt;
      <ul>
        <li v-for="hobbies in hobbies" :key="hobbies.id">{{ hobbies }}</li>
      </ul>
    </article>
  </main>
</template>

<style>
* { box-sizing: border-box; }
body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: #db00ff;
  color: #192d3a;
}
main { min-height: 100vh; display: grid; place-items: center; padding: 24px; }
.card { width: 100%; max-width: 520px; padding: 16px; background: white; border-radius: 6px; }
.eyebrow { color: #24634a; font-size: 12px; font-weight: bold; letter-spacing: 2px; }
h1 { overflow-wrap: anywhere; font-size: 32px; font-weight: 200; }
label { display: block; margin-top: 24px; font-weight: bold; }
input { width: 100%; padding: 12px; margin-top: 8px; border: 1px solid #637580; border-radius: 8px; font: inherit; }
button { padding: 12px 16px; margin: 16px 8px 0 0; border: 0; border-radius: 8px; background: #04ff00; color: white; font: inherit; cursor: pointer; }
button:hover { background: #174630; }
:focus-visible { outline: 3px solid #b55000; outline-offset: 3px; }
/* TASK 3: Personalise the background, card, heading and buttons. */
</style>
-->

<script>
import {ref, computed} from 'vue'

const newExercise = ref('')
const newMinutes = ref(15)
const errorMessage = ref('')
let nextId = 3
const exercises = ref([
  {id: 1, name: 'Walking', minutes: 20, completed: false},
  {id: 2, name: 'Stretching', minutes: 10, completed: false}
])

function addExercise() {
  const exerciseName = newExercise.value.trim()
  const minutes = Number(newMinutes.value)
  if (!exerciseName) {
    errorMessage.value = 'Please enter an exercise name.'
    return
  }
  if (!Number.isInteger(minutes) || minutes < 1 || minutes > 180) {
    errorMessage.value = 'Enter a whole number from 1 to 180 minutes.'
    return
  }
  exercises.value.push({
    id: nextId++,
    name: exerciseName,
    minutes,
    completed: false
  })
  newExercise.value = ''
  newMinutes.value = 15
  errorMessage.value = ''
}

</script>


<template>
  <main class="dashboard">
    <header class="hero">
      <p class="eyebrow">YOUR DAILY WORKOUT PLANNER</p>
      <h1>Shape Up</h1>
      <p>Small steps. Stronger habits.</p>
    </header>
    <!-- STEP 7: Progress summary goes here. -->
    <div class="dashboard-grid">
      <section class="panel">
        <h2>Plan an exercise</h2>
        <!-- STEP 5: Form goes here. -->
        <form @submit.prevent="addExercise">
          <label for="exercise-name">Exercise name</label>
          <input id="exercise-name" v-model="newExercise" type="text"
                 placeholder="For example, cycling" maxlength="60" required>
          <label for="exercise-minutes">Duration in minutes</label>
          <input id="exercise-minutes" v-model.number="newMinutes"
                 type="number" min="1" max="180" step="1" required>
          <button type="submit" class="primary-button">Add exercise</button>
          <p v-if="errorMessage" class="error-message" role="alert">
            {{ errorMessage }}
          </p>
        </form>




      </section>
      <section class="panel">
        <h2>Your workout</h2>
        <!-- STEP 4: Exercise list goes here. -->
        <p v-if="exercises.length === 0" class="empty-state">
          No exercises yet.Add one to start your plan.
        </p>

        <ul v-else class="exercise-list">
          <li v-for="exercise in excercises" :key="exercise.id"
              class="exercise"

              :class="{completed: exercise.completed}">

            <label class="exercise-details">
              <input type="checkbox" v-model="exercise.completed">
              <span>
                <strong>{{ exercise.name }}</strong>
                <small>{{ exercise.minutes }} minutes</small>
              </span>
            </label>
            <!-- STEP 6: Remove button goes here. -->
          </li>
        </ul>

      </section>
    </div>
  </main>
</template>


<style>

</style>