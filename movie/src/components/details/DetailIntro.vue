<script>
export default {
  props: {
    movieBasic: {
      type: Object,
      required: true
    }
  }
}
</script>

<template>
  <div class="movie__detail__intro">
    <div class="intro__wrap">
      <div class="backDrop">
        <img
          :src="'https://image.tmdb.org/t/p/w500' + movieBasic.backdrop_path"
          class="back"
          alt=""
        />
        <div class="intro__img">
          <img :src="'https://image.tmdb.org/t/p/w500' + movieBasic.poster_path" alt="" />
        </div>
        <div class="intro__text">
          <div class="intro__title">
            <h3>{{ movieBasic && movieBasic.original_title }}</h3>
          </div>
          <div class="intro__desc">
            <span>#{{ movieBasic.tagline }}#</span>

            <span>{{ movieBasic.overview }}</span>
            <span>
              <ul class="desc__info">
                <li class="movie__genre">
                  장르:
                  <em v-for="(genre, index) in movieBasic?.genres || []" :key="index">
                    {{ genre.name }}{{ index < movieBasic.genres.length - 1 ? ', ' : '' }}
                  </em>
                </li>
                <li class="movie__everge">
                  평점: <em>{{ movieBasic.vote_average }}</em>
                </li>
                <li class="movie__">
                  개봉일: <em>{{ movieBasic.release_date }}</em>
                </li>
              </ul>
            </span>
          </div>
          <div class="btn">
            <button class="watch">watch</button>
            <button class="add">add</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<style lang="scss">
.movie__detail__intro {
  width: 100%;

  .backDrop {
    position: relative;
    background-image: linear-gradient(
      to right,
      rgba(31.5, 10.5, 10.5, 1) calc((100vw - 170px) - 340px),
      rgba(31.5, 10.5, 10.5, 0.84) 50%,
      rgba(31.5, 10.5, 10.5, 0.84) 100%
    );
    .back {
      height: 60vh;
      opacity: 0.3;
    }

    .intro__img {
      width: 50%;
      position: absolute;
      left: 15%;
      top: 17%;
      img {
        width: 30vh;
        height: 40vh;
      }
    }
    .intro__text {
      position: absolute;
      left: 44%;
      top: 17%;
      width: 50%;
      height: 38vh;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      padding: 0.5rem;

      .intro__title {
        h3 {
          font-size: 2rem;
          font-weight: 600;
        }
      }
    }
    .intro__desc {
      display: flex;
      flex-direction: column;
      span {
        display: inline-block;
        width: 100%;
        padding: 1rem 0;
        ul {
          width: 80%;
          display: flex;
          justify-content: space-between;
        }
      }
    }
  }
}
</style>
