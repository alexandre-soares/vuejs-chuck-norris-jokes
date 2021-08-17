<template>
  <div class="navbar">
    <h1>
      Chuck Norris Jokes App
      <img
        src="https://assets.chucknorris.host/img/avatar/chuck-norris.png"
        alt="logo"
      />
    </h1>
    <ul class="nav">
      <router-link tag="li" to="/">Home</router-link>
      <router-link tag="li" to="/search">Search</router-link>
    </ul>
  </div>
</template>

<script></script>

<style lang="scss" scoped>
.navbar {
  padding: 2rem 4rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: white;

  & h1 {
    display: flex;
    align-items: center;

    & img {
      margin-left: 2rem;
    }
  }
}

.nav {
  display: flex;

  & a {
      margin: 0 3rem;
      font-size: 1.4rem;
      text-decoration: none;
      color: black;

      &:last-child{
          margin-right: 0;
      }
  }
}
</style>
