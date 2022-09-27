<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <header>
    <div class="site">
      <div class="name">To-Do List</div>
      <div class="description">I know, you'll never use it but hey, that's a to-do list.</div>
    </div>
    <nav>
      <RouterLink to="/">Home</RouterLink>
    </nav>
  </header>
  <main>
    <RouterView />
  </main>
  
</template>

<style lang="scss" scoped>
@import url(https://fonts.googleapis.com/css?family=Poppins:100,100italic,200,200italic,300,300italic,regular,italic,500,500italic,600,600italic,700,700italic,800,800italic,900,900italic);

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font: {
    family: 'Poppins', sans-serif;
  }

  &::selection {
    background: transparentize(#42B883, 0.5);
  }
}

a {
  text-decoration: none;
}

header {
  background: transparentize(#4275b8, 0.5);
  padding: .5rem 0 .5rem 0;
  border-radius: .5rem;
  .site {
    display: flex;
    justify-content: space-evenly;

    .name {
      font-weight: 500;
    }
  }

  nav {
    display: flex;
    justify-content: space-around;
    margin: .25rem 0 .25rem 0;
    padding: .25rem;
    border-radius: .5rem;

    a {
      color: rgb(250, 250, 250);
    }
  }
}
</style>
