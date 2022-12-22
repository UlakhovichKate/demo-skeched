<template>
  <div class="home">
    <h1 class="home__title">Sketched by siena demo vue js</h1>
    <a href="#/builder" class="home__btn" type="button">Start</a>
  </div>
</template>

<script>
export default {
  name: "Home"
}
</script>

<style scoped>
  .home {
    width: 100%;
    height: calc(100vh - 60px);
    padding: 50px 15px;
    background-color: #F3F3F3;
    font-family: 'Roboto', sans-serif;
  }

  .home__title {
    font-weight: 500;
    font-size: 40px;
    line-height: 40px;
    text-align: center;
    letter-spacing: -0.22px;
    text-transform: uppercase;
  }

  .home__btn {
    display: flex;
    justify-content: center;
    align-items: center;
    max-width: 345px;
    margin: 50px auto 0;
    padding: 19px 25px;
    background: #FFBD9B;
    border-radius: 25px;
    font-size: 11px;
    line-height: 12px;
    text-align: center;
    letter-spacing: 0.04em;
    text-transform: uppercase;
    color: #000;
    text-decoration: none;
  }

  .home__btn:hover {
    opacity: 0.8;
  }
</style>
