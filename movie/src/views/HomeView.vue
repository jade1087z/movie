<script setup>
import axios from 'axios'
import { onMounted, ref } from 'vue'
import HeaderSection from '../components/section/HeaderSection.vue'
import FooterSection from '../components/section/FooterSection.vue'
import MovieSearch from '../components/contents/MovieSearch.vue'
import MovieTag from '../components/contents/MovieTag.vue'
import MovieCont from '../components/contents/MovieCont.vue'

// const movies = ref([])
// const searchQuery = ref('')

// const searchMovies = async (query) => {
//   const url = 'https://api.themoviedb.org/3/search/movie'

//   try {
//     const response = await axios.get(url, {
//       params: {
//         api_key: 'b7925d74a78291f6b602f9e51430a5ed',
//         language: 'ko-kr',
//         page: 1,
//         query
//       }
//     })
//     movies.value = response.data.results
//   } catch (error) {
//     console.log(error)
//   }
// }

// const fetchMovies = async (category, query) => {
//   let url = 'https://api.themoviedb.org/3/movie/popular'
//   switch (category) {
//     case 'latest':
//       url = 'https://api.themoviedb.org/3/movie/now_playing'
//       break
//     case 'popular':
//       url = 'https://api.themoviedb.org/3/movie/popular'
//       break
//     case 'upcoming':
//       url = 'https://api.themoviedb.org/3/movie/upcoming'
//       break
//   }

//   try {
//     const response = await axios.get(url, {
//       params: {
//         api_key: 'b7925d74a78291f6b602f9e51430a5ed',
//         language: 'ko-kr',
//         page: 1
//       }
//     })
//     console.log(response)
//     movies.value = response.data.results
//     console.log(movies)
//   } catch (error) {
//     console.log(error)
//   }
// }
// onMounted(async () => {
//   // 초기 페이지 로딩 시 최신 영화를 가져옴
//   await fetchMovies('latest')
// })
</script>

<template>
  <HeaderSection />
  <main id="main" role="main">
    <div class="container">
      <div class="movie__inner">
        <MovieSearch />
        <!-- search -->

        <MovieTag />
        <!-- tag -->

        <MovieCont />
        <!-- conts -->
      </div>
    </div>
    <TheWelcome />
  </main>
  <FooterSection />
</template>

<script>
export default {
  name: 'Movie Home Page',
  components: {
    HeaderSection,
    FooterSection,
    MovieSearch,
    MovieTag,
    MovieCont,
    MovieCont
  },
  data() {
    return {
      movies: []
    }
  },
  methods: {
    async search(query) {
      try {
        const response = await fetch(
          `https://api.themoviedb.org/3/search/movie?api_key=b7925d74a78291f6b602f9e51430a5ed&language:'ko-KR'&query=${query}`
        )
        const result = await response.json()
        console.log(result)
      } catch (error) {
        console.log(error)
      }
    },
    async tags(query) {
      try {
        const response = await fetch(
          `https://api.themoviedb.org/3/search/movie?api_key=b7925d74a78291f6b602f9e51430a5ed&language:'ko-KR'&query=${query}`
        )
        const result = await response.json()
        console.log(result)
      } catch (error) {
        console.log(error)
      }
    }
    // async contents(query) {
    //   try {
    //     const response = await fetch(`https://api.themoviedb.org/3/search/movie`)
    //     const result = await response.json()
    //     console.log(result)
    //   } catch (error) {
    //     console.log(error)
    //   }
    // }
  }
}
</script>
<style lang="scss">
.movie__search {
  padding-top: 20px;
  margin-bottom: 20px;
  position: relative;
  input {
    border-radius: 35px;
    width: 90%;
    height: 50px;
    margin-left: 3rem;
    padding-left: 1rem;
  }
  button {
    position: absolute;
    left: 88.5%;
    top: 37%;
    font-size: 0.9rem;
    border-radius: 25px;
    padding: 0.5rem;
    background-color: var(--white);
    color: var(--black200);
  }
}
.movie__tag {
  ul {
    display: flex;
    justify-content: start;
    margin-left: 3rem;
  }

  li {
    z-index: 10000;
    cursor: pointer;
    a {
      font-family: var(--mainfont-nanum);
      font-weight: bold;
      padding: 0.5rem;
      display: inline-block;
      border-radius: 50px;
      border: 1px solid var(--white);
      margin: 15px 10px 20px 0;
      color: var(--white);

      &:hover {
        background-color: var(--white);
        color: var(--black);
      }
    }
  }
}

.movie__cont {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
  .movie {
    width: 24%;
    margin-bottom: 7rem;
    margin-top: 1rem;
    height: 400px;
    cursor: pointer;

    img {
      border-radius: 50px;

      &:hover {
      }
    }
  }
}
</style>
