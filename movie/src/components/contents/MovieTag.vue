<template>
  <div class="movie__tag">
    <ul>
      <li><a href="#" @click="fetchMovies('latest')">최신영화</a></li>
      <li><a href="#" @click="fetchMovies('popular')">인기영화</a></li>
      <li><a href="#" @click="fetchMovies('upcoming')">개봉예정</a></li>
      <li><a href="#">액션영화</a></li>
      <li><a href="#">슬픈영화</a></li>
    </ul>
  </div>
</template>
