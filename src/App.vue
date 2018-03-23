<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">地图</router-link> |
      <router-link to="/tool">画图工具</router-link>
    </div>
    <router-view/>

  </div>
</template>

<style lang="stylus">
  @import '../src/assets/bootstrap/css/bootstrap.css';
  @import '../src/assets/bootstrap/css/bootstrap-theme.css';

  #app
  font-family 'Avenir', Helvetica, Arial, sans-serif
  -webkit-font-smoothing antialiased
  -moz-osx-font-smoothing grayscale
  text-align center
  color #2c3e50

  #nav
    padding 30px
    a
      font-weight bold
      color #2c3e50
      &.router-link-exact-active
        color #42b983
</style>
