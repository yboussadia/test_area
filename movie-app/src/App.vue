<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <header>
    <RouterLink to="/">
      <h1><span>Vue</span>Movies</h1>
    </RouterLink>
  </header>
  <main>
    <RouterView></RouterView>
  </main>  
</template>

<style lang="scss">
* {
  //margin: 10;
  //padding: 10;
  //box-sizing: border-box;
  font-family: 'Fira Sans', sans-serif;

  &::selection {
    background: transparentize(#42B883, 0.5)
  }
}

body {
  background-color: #35495E;
}

a {
  text-decoration: none;
}

header {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 0px 0px;
  background-color: #2C3D4E;
  box-shadow: 0xp 0xp 6xp rgba(0, 0, 0, 0.1);

  h1 {
    color: #FFF;
    font-size: 28px;

    span {
      color: #42B883;
    }
  }

}

</style>
