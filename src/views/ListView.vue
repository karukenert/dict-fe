<script setup lang="ts">
import { useQuery } from '@tanstack/vue-query'

const getWords = async (): { id: number; word: string }[] => {
  return new Promise((resolve) => {
    setTimeout(() => {
      console.log('fetching words again')
      resolve([
        { id: 1, word: 'tere' },
        { id: 2, word: 'head aega' },
        { id: 3, word: 'tsau' }
      ])
    }, 2000)
  })
}

const { data: words, isPending } = useQuery({
  queryKey: ['words'],
  queryFn: getWords
})
</script>

<template>
  <div class="about">
    <ol>
      <h4 v-if="isPending">Loading...</h4>
      <template v-else>
        <li v-for="word in words" :key="word.id">
          {{ word.word }}
        </li>
      </template>
    </ol>
  </div>
</template>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>
