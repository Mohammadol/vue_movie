<template>
  <header>
    <router-link to="/">
      <h1><span>vue</span>movies</h1>
    </router-link>
  </header>
  <main>
    <router-view />
  </main>
  <footer></footer>
</template>

<style lang="scss">
* {
  margin: 0px;
  padding: 0px;
  box-sizing: border-box;
  font-family: "fira sans", sans-serif;
  &::selection {
    background: transparentize($color: #42b883, $amount: 0.5);
  }
  body {
    background-color: #35495e;
  }
  a {
    text-decoration: none;
  }
  header {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 10px 16px;
    background-color: #2c3d4e;
    box-shadow: 0px, 0px, 6px rgb(0, 0, 0, 0.1);
    h1 {
      color: white;
      span {
        color: #42b883;
      }
    }
  }
}
</style>
