<template>
  <section class="movie__search">
    <h2 class="blind">검색하기</h2>
    <input
      type="text"
      placeholder="찾으시려는 작품 제목을 입력해주세요."
      v-model="searchQuery"
      @keyup.enter="searchMovies(searchQuery)"
    />
    <button type="submit" @click="searchMovies(searchQuery)">검색</button>
  </section>
</template>

<script>
export default {}
</script>
