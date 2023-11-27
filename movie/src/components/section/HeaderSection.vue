<template>
  <header id="header" role="banner">
    <div class="header__inner container">
      <div class="header__intro">
        <h2 class="logo"><a href="/">NETFILX</a></h2>
        <nav>
          <ul class="menu">
            <li v-for="(item, index) in menuItems" :key="index">
              <a
                href="#"
                @mouseover="changeColor(index)"
                @mouseout="resetColor"
                :class="{ inactive: activeIndex >= 0 && activeIndex !== index }"
              >
                {{ item }}
              </a>
            </li>
          </ul>
        </nav>
      </div>
    </div>
    <div class="header__banner">
      <img src="../../assets/img/back.jpg" alt="" />
      <div class="movie__banner">
        <div class="header__movie">
          <img src="../../assets/img/poster.jpg" alt="" />
        </div>
        <div class="movie__text">
          <div class="movie__title">Oppenheimer</div>
          <div class="movie__desc">
            세상을 구하기 위해 세상을 파괴할 지도 모르는 선택을 해야 하는 천재 과학자의 핵개발
            프로젝트.
          </div>
          <div class="movie__infomation">
            <div class="average">평점: <em>8.1</em></div>
            <div class="date">개봉일: <em>2023-07-19</em></div>
          </div>
          <div class="movie__actor">
            <ul>
              <li><img src="../../assets/img/poster.jpg" alt="" /></li>
              <li><img src="../../assets/img/poster.jpg" alt="" /></li>
              <li><img src="../../assets/img/poster.jpg" alt="" /></li>
              <li><img src="../../assets/img/poster.jpg" alt="" /></li>
            </ul>
          </div>
          <div class="movie__btn">
            <button class="watch">> watch</button>
            <button class="add">+ add List</button>
          </div>
        </div>
      </div>
    </div>
  </header>
</template>
<script setup>
import { ref } from 'vue'

const menuItems = ['Home', 'Movies', 'Service', 'MyPage']
const activeIndex = ref(-1)

const changeColor = (index) => {
  activeIndex.value = index
}

const resetColor = () => {
  activeIndex.value = -1
}
</script>
<style lang="scss">
#header {
  width: 100%;
  padding: 30px;
  color: white;
}
.header__inner {
}
.header__intro {
  display: flex;
  justify-content: space-between;
}
.logo {
  width: 50%;
  font-weight: bold;
  font-size: 24px;
  cursor: pointer;
  a:hover {
    color: red;
  }
}

nav {
  display: flex;

  width: 50%;
}
nav ul {
  display: flex;
  justify-content: flex-end;
}
nav .menu {
  width: 100%;
}
nav .menu li {
  padding: 1rem;
}
nav .menu li a {
  position: relative;
  transition: all 0.2s;
}
.menu li a {
  color: white;
}

.menu li a.active {
  color: #22242a;
}

.menu li a.inactive {
  color: var(--black400);
}

nav .menu li a::before {
  content: '';
  position: absolute;
  width: calc(100% - 9px);
  height: 2px;
  background-color: var(--white100);
  left: 9%;
  top: 130%;
  transition: all 0.3s;
  transform: scaleX(0);
}
nav .menu li a:hover::before {
  transform: scaleX(1);
}

.header__banner {
  width: 100%;
  height: 600px;
  margin-top: 50px;
  position: relative;
  //   background-image: url('../../assets/img/back.jpg');
  //   background-repeat: no-repeat;
  //   background-size: contain;
}
.header__banner img {
  width: 100%;
  height: inherit;
  //   filter: blur(5px);
}
.movie__banner {
  width: 100%;
  height: inherit;
  display: flex;
}
.header__movie {
  width: 50%;
  position: absolute;
  left: 5%;
  top: 10%;
}
.header__movie img {
  width: 30vw;
  height: 60vh;
}
.movie__text {
  width: 50%;
  height: 80%;
  position: absolute;
  left: 50%;
  top: 7%;
  display: flex;
  flex-direction: column;
  justify-content: space-around;

  .movie__infomation {
    width: 100%;
    display: flex;
    font-weight: 600;
    font-size: 0.8rem;
    div {
      padding: 1rem;
    }
  }

  .movie__actor {
    ul {
      width: 100%;
      display: flex;
      justify-content: space-around;
      li {
        width: 20%;
        height: 120px;
        background-color: #fff;
        margin-right: 20px;
      }
    }
  }

  .movie__title {
    font-size: 2rem;
    font-weight: 600;
    padding: 1rem;
  }
  .movie__desc {
    font-size: 0.9rem;
    font-weight: 600;
    padding: 1rem;
  }
  .movie__btn {
    margin-top: 30px;

    button {
      width: 125px;
      height: 40px;
      padding-bottom: 5px;
      padding-right: 10px;
      border-radius: 15px;
      font-size: 1rem;
      transition: all 0.4s;
      filter: blur(0.2px);
      font-weight: 400;
    }

    .watch {
      margin-right: 50px;
      background-color: var(--red);
      color: var(--white100);
      &:hover {
        background-color: var(--red-hover);
        color: white;
      }
    }
    .add {
      background-color: var(--black300);
      color: var(--white100);
      &:hover {
        background-color: var(--black400);
        color: var(--primary-color);
      }
    }
  }
}
</style>
