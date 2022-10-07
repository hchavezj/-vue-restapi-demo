<script setup>
import { onMounted, onUnmounted } from 'vue'
import { useRoute } from 'vue-router'

import useCharacters from '@/composables/useCharacters'

const route = useRoute()
const { fetchCharacter, currentCharacter } = useCharacters()

onMounted(async () => {
  await fetchCharacter(route.params.id)
})

onUnmounted(() => {
  currentCharacter.value = null
})
</script>

<template>
  <main
    class="min-h-screen bg-gradient-to-r from-fuchsia-900 to-red-700 py-8 text-white"
  >
    <div
      v-if="currentCharacter"
      class="flex flex-col items-center justify-center gap-6"
    >
      <img :src="currentCharacter.imageUrl" :alt="currentCharacter.name" />
      <h1 class="text-white-800 text-6xl font-bold">
        Hi, I'm {{ currentCharacter.name }}
      </h1>
      <ul v-if="currentCharacter.films.length > 0">
        <li>Films</li>
        <li v-for="films in currentCharacter.films" :key="films.id">
          {{ films }}
        </li>
      </ul>
      <h1 v-else>No Films</h1>
      <ul v-if="currentCharacter.shortFilms.length > 0">
        <li>Short Films</li>
        <li
          v-for="shortFilms in currentCharacter.shortFilms"
          :key="shortFilms.id"
        >
          {{ shortFilms }}
        </li>
      </ul>
      <h1 v-else>No Short Films</h1>
      <ul v-if="currentCharacter.tvShows.length > 0">
        <li text-center>TV Shows</li>
        <li v-for="tvShows in currentCharacter.tvShows" :key="tvShows.id">
          {{ tvShows }}
        </li>
      </ul>
      <h1 v-else>No TV Shows</h1>
      <pre>{{ currentCharacter }}</pre>
    </div>
  </main>
</template>
