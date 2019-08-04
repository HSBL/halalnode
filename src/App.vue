<template>
  <div id="app">
    <appheader v-on:emitSignin="changeSignin()" v-on:emitLogout="changeLogout()" v-bind:output="output" />
    <div id="nav">
      <router-link to="/">Home</router-link>|
      <router-link v-if="this.output" to="/about">Certification</router-link>
    </div>
    <router-view />
    <Login v-on:emitSignedin="changeSignedin($event)" v-if="this.signin" />
  </div>
</template>
<script>
import appheader from "@/components/Header.vue";
import Login from "@/components/Login.vue";

export default {
  components: {
    appheader,
    Login
  },
  data() {
    return {
      signin: false,
      logout: true,
      output: null
    };
  },
  methods: {
    changeSignin: function() {
      this.signin = !this.signin;
    },
    changeSignedin: function(eventData){
      this.output = eventData;
    },
    changeLogout: function() {
      this.logout = !this.logout;
    }
  }
};
</script>

<style lang="scss">
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#nav {
  padding: 30px;
  a {
    font-weight: bold;
    color: #2c3e50;
    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
