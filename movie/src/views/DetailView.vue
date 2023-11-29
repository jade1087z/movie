<script setup>
import HeaderSection from '../components/section/HeaderSection.vue'

import { ref, onMounted } from 'vue'
import { useRouter, useRoute } from 'vue-router'
import axios from 'axios'

const router = useRouter()
const route = useRoute()
const movieDetail = ref(null)
const movieWatch = ref(null)

onMounted(async () => {
  const movieId = route.params.movieId
  console.log(movieId)
  const detailResponse = await axios.get(`https://api.themoviedb.org/3/movie/${movieId}`, {
    params: {
      language: 'ko-KR',
      api_key: 'b7925d74a78291f6b602f9e51430a5ed'
    }
  })
  movieDetail.value = detailResponse.data
  console.log(movieDetail.value)

  const watchResponse = await axios.get(
    `https://api.themoviedb.org/3/movie/${movieId}/watch/providers`,
    {
      params: {
        api_key: 'b7925d74a78291f6b602f9e51430a5ed'
      }
    }
  )

  movieWatch.value = watchResponse.data
  console.log(movieWatch.value)
  const watchResult = movieWatch.value
  console.log(watchResult)
})
</script>

<template>
  <HeaderSection />
  <div></div>
</template>
