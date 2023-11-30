<template>
  <header id="header_g" role="banner">
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
#header_g {
  width: 100%;
  padding: 30px;
  color: white;

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
}
</style>
