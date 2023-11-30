<template>
  <HeaderNav />
  <div>
    <main id="main">
      <DetailIntro v-if="movieBasic" :movieBasic="movieBasic" />
      <DetailInfo v-if="movieInfo" :movieInfo="movieInfo" />
      <DetailReview v-if="movieReview" :movieReview="movieReview" />
      <DetailCredits v-if="movieCredits" :movieCredits="movieCredits" />
    </main>
  </div>
</template>

<script>
import { onMounted, ref } from 'vue'
import { useRoute } from 'vue-router'
import axios from 'axios'

import DetailInfo from '../components/details/DetailInfo.vue'
import DetailReview from '../components/details/DetailReview.vue'
import DetailCredits from '../components/details/DetailCredits.vue'
import DetailIntro from '../components/details/DetailIntro.vue'
import HeaderNav from '../components/section/HeaderNav.vue'

export default {
  name: 'MovieDetailPage',

  components: {
    DetailIntro,
    DetailInfo,
    DetailReview,
    DetailCredits,
    HeaderNav
  },

  setup() {
    const movieBasic = ref(null)
    const movieInfo = ref(null)
    const movieReview = ref(null)
    const movieCredits = ref(null)

    const route = useRoute()

    onMounted(async () => {
      const movieId = route.params.movieId
      const apiKey = import.meta.env.VITE_API_KEY
      const language = 'ko-KR'

      try {
        const resMovieBasic = await axios.get(
          `https://api.themoviedb.org/3/movie/${movieId}?language=${language}&api_key=${apiKey}`
        )
        movieBasic.value = resMovieBasic.data
        console.log(resMovieBasic.data)

        const resMovieInfo = await axios.get(
          `https://api.themoviedb.org/3/movie/${movieId}?language=${language}&api_key=${apiKey}`
        )
        movieInfo.value = resMovieInfo.data
        console.log(resMovieInfo.data)

        const resMovieReview = await axios.get(
          `https://api.themoviedb.org/3/movie/${movieId}/reviews?language=${language}&api_key=${apiKey}`
        )
        movieReview.value = resMovieReview.data
        console.log(resMovieReview.data)

        const resMovieCredits = await axios.get(
          `https://api.themoviedb.org/3/movie/${movieId}/credits??language=${language}&api_key=${apiKey}`
        )
        movieCredits.value = resMovieCredits.data
        console.log(resMovieCredits.data)
      } catch (err) {
        console.log(err)
      }
    })

    return { movieBasic, movieInfo, movieReview, movieCredits }
  }
}
</script>

<style lang="scss">
.detail__intro {
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center;
  position: relative;
  padding: 30px;

  &::before {
    content: '';
    width: 100%;
    height: 100%;
    position: absolute;
    left: 0;
    top: 0;
    background-color: #00000032;
    backdrop-filter: blur(7px);
    z-index: 1;
  }

  .container {
    display: flex;
    justify-content: space-between;
    position: relative;
    z-index: 10;

    .left {
      width: 350px;
    }

    .right {
      width: calc(100% - 390px);

      h2 {
        font-size: 30px;
        margin-bottom: 10px;
      }

      .desc {
        margin-bottom: 10px;
      }

      .average {
        margin-bottom: 20px;
      }

      .credits {
        display: flex;

        div {
          width: 100px;
          margin-right: 10px;
        }
      }
    }
  }
}
</style>
