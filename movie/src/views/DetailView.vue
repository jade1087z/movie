<script setup>
import HeaderSection from '../components/section/HeaderSection.vue'

import { ref, onMounted, toRefs } from 'vue'
import { useRouter, useRoute } from 'vue-router'
import axios from 'axios'

const router = useRouter()
const route = useRoute()
const movieWatch = ref(null)
const movieDetail = ref(null)

onMounted(async () => {
  const movieId = route.params.movieId

  const detailResponse = await axios.get(`https://api.themoviedb.org/3/movie/${movieId}`, {
    params: {
      language: 'ko-KR',
      api_key: 'b7925d74a78291f6b602f9e51430a5ed'
    }
  })
  movieDetail.value = detailResponse.data
  console.log(movieDetail.value)
  const detail = movieDetail.value

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

  return {
    movieDetail: movieDetail.value,
    movieWatch: movieWatch.value
  }
})
</script>

<template>
  <HeaderSection />
  <section id="movie__detail">
    <div class="detail__inner container">
      <div class="tab__wrap">
        <div class="detail__tab">
          <ul>
            <li class="on">
              <a href="#">주요정보</a>
            </li>
            <li class="">
              <a href="#">무비포스트</a>
            </li>
            <li class="">
              <a href="#">관람평</a>
            </li>
            <li class="">
              <a href="#">예고편/스틸컷</a>
            </li>
          </ul>
        </div>
        <div class="detail__wrap">
          <div class="detail__summary">
            <div class="summary__text">
              <div class="summary__main">
                <h3>{{ movieDetail && movieDetail.tagline }}</h3>
                <div class="infomation">
                  <p>
                    장르:
                    <em v-for="(genre, index) in movieDetail?.genres || []" :key="index">
                      {{ genre.name }}{{ index < movieDetail.genres.length - 1 ? ', ' : '' }}
                    </em>
                  </p>
                  <p>
                    관람 등급:
                    <em>{{
                      movieDetail && movieDetail.adult ? '전체 관람가능' : '청소년 관람불가'
                    }}</em>
                  </p>
                </div>
              </div>
              <span>{{ movieDetail && movieDetail.overview }}</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style lang="scss">
#movie__detail {
  color: var(--white100);
  width: 100%;
  .detail__inner {
    .tab__wrap {
      .detail__tab {
        width: 100%;
        display: flex;
        justify-content: center;
        ul {
          width: 100%;
          display: flex;
          justify-content: space-around;

          li {
            display: block;
            width: 100%;
            height: 41px;
            text-align: center;
            line-height: 38px;
            color: var(--white100);
            font-size: 1.02rem;
            font-weight: 600;
            border: 2px solid var(--black500);
            cursor: pointer;
            transition: all 0.2s;
            &:hover {
              background-color: var(--white100);
              color: var(--black300);
            }
          }

          .on {
            color: var(--black400);
            border-color: var(--white100);
            background-color: var(--white100);
            font-weight: bold;
            font-size: 1.1rem;
          }
        }
      }
      // tab end
      .detail__wrap {
        .detail__summary {
          margin: 20px 0 0 0;

          .summary__text {
            overflow: hidden;
            height: 150px;

            .summary__main {
              width: 100%;
              display: flex;
              justify-content: space-between;

              h3 {
                font-size: 1.2rem;
                font-weight: 600;
                margin-bottom: 50px;
              }
              .infomation {
                width: 35%;
                display: flex;
                justify-content: space-between;

                p {
                  font-size: 0.8rem;
                }
              }
            }

            span {
              font-size: 0.9rem;
              font-weight: 300;
            }
          }
        }
      }
    }
  }
}
</style>