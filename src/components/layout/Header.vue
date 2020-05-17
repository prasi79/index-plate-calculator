<template>
  <nav>
    <a class="burger-nav" v-on:click="navbarOpen = !navbarOpen"></a>
    <ul v-bind:class="{ open: navbarOpen }">
      <li><router-link to="/" exact>Calculator</router-link></li>
      <li><router-link to="/holecircles" exact>Holecircles</router-link></li>
      <li><router-link to="/settings" exact>Settings</router-link></li>
    </ul>
  </nav>
</template>

<script>
export default {
  name: "Header",
  data() {
    return {
      navbarOpen: false
    };
  }
};
</script>

<style scoped lang="scss">
$breakpoint-tablet: 650px;
$breakpoint-phone: 500px;

nav {
  background: rgba(160, 105, 255, 0.1);
  padding: 5px 0;
  ul {
  text-align: right;
  margin: 0;
    li {
    display: inline;
    margin: 0 10px;
    font-family: Arial, Helvetica, sans-serif;
    font-size: 20px;
      a {
      color: rgb(160, 105, 255);
      text-decoration: none;
      padding: 6px 0px;
      font-weight: normal;
      }
    }
  }
}

.router-link-active {
  background: #eee;
  color: #444;
}

@media(max-width: $breakpoint-tablet) {
  nav {
    ul {
      text-align: center;
      position: relative;
      right: 25px;
    }
  }
}

@media (max-width: $breakpoint-phone) {
  nav {
    width: 100%;
    padding: 0;
    .burger-nav {
      display: block;
      height: 40px;
      width: 100%;
      background: url(../../assets/icons/burger.png) no-repeat 98% center;
      cursor: pointer;
      
    }
    ul {
      overflow: hidden;
      height: 0;
      li {
        float: none;
        text-align: left;
        width: 100%;
        margin: 0px;
        display: block;
        a {
          padding: 10px;
          display: block;
          margin: 0;
        }
      }
    }
    .open {
        height: auto;
        position: relative;
        right: 40px;
        width: 100%;
      }
  }
}


</style>