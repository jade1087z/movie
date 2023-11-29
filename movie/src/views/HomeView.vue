<script setup>
import { ref, onMounted } from 'vue'
import axios from 'axios'
import HeaderSection from '@/components/section/HeaderSection.vue'
import FooterSection from '@/components/section/FooterSection.vue'

const movies = ref([])
const searchKeyword = ref('')

const fetchMovies = async (category) => {
  let url = 'https://api.themoviedb.org/3/movie/popular'

  switch (category) {
    case 'latest':
      url = 'https://api.themoviedb.org/3/movie/now_playing'
      break
    case 'popular':
      url = 'https://api.themoviedb.org/3/movie/popular'
      break
    case 'upcoming':
      url = 'https://api.themoviedb.org/3/movie/upcoming'
      break
    case 'toprated':
      url = 'https://api.themoviedb.org/3/movie/top_rated'
      break
  }

  try {
    const response = await axios.get(url, {
      params: {
        api_key: '9278d13f704ad0fe53c2263b692efd89',
        language: 'ko-KR',
        page: '1'
      }
    })
    movies.value = response.data.results
    console.log(response.data.results)
  } catch (err) {
    console.log(err)
  }
}

const serachMovies = async () => {
  try {
    const response = await axios.get('https://api.themoviedb.org/3/search/movie', {
      params: {
        api_key: '9278d13f704ad0fe53c2263b692efd89',
        language: 'ko-KR',
        query: searchKeyword.value
      }
    })
    movies.value = response.data.results
  } catch (err) {
    console.error(err)
  }
}

onMounted(async () => {
  await fetchMovies('latest')
})
</script>

<template>
  <HeaderSection />
  <main id="main" role="main">
    <div class="container">
      <div class="movie__inner">
        <section class="movie__search">
          <h2 class="blind">검색하기</h2>
          <input
            type="search"
            v-model="searchKeyword"
            placeholder="검색어를 입력해주세요!"
            @keyup.enter="serachMovies"
          />
          <button type="submit" @click="serachMovies">검색</button>
        </section>
        <!-- //movie__search -->

        <div class="movie__tag">
          <ul>
            <li><a href="#" @click="fetchMovies('latest')">최신 영화</a></li>
            <li><a href="#" @click="fetchMovies('popular')">인기 영화</a></li>
            <li><a href="#" @click="fetchMovies('upcoming')">개봉 예정</a></li>
            <li><a href="#" @click="fetchMovies('toprated')">최고 평점</a></li>
          </ul>
        </div>
        <!-- //movie__tag -->

        <section class="movie__cont">
          <h2 class="blind">영화</h2>
          <div class="movie play__icon" v-for="movie in movies" :key="movie.id">
            <a :href="'/detail/' + movie.id">
              <img
                :src="'https://image.tmdb.org/t/p/w500' + movie.poster_path"
                :alt="movie.title"
              />
            </a>
          </div>
        </section>
        <!-- //movie__cont -->
      </div>
    </div>
  </main>
  <FooterSection />
</template>

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
