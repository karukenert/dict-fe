<script setup lang="ts">
import { useMutation } from '@tanstack/vue-query'
import { ref, computed } from 'vue'

interface RequestBody {
  id?: number
  word: string
}

const addWord = async (wordData: RequestBody) => {
  return new Promise((resolve) => {
    setTimeout(() => {
      console.log(wordData)
      resolve(1)
    }, 2000)
  })
}

const mutation = useMutation({
  mutationFn: addWord
})

const inputValue = ref('')

const mutata = () => {
  mutation.mutate({ word: inputValue.value })
}

const isLoading = computed(() => (mutation.isPending ? 'yup' : 'nope'))
</script>

<template>
  <main>
    <input type="text" v-model="inputValue" />
    <button @click="mutata">Refetch</button>
    <br />
    {{ { pending: mutation.isPending } }}

    {{ isLoading }}
  </main>
</template>
