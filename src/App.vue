<template>
  <div>
    @{{user.username}} - {{fullName}}
  </div>
</template>

<script>


export default {
  name: 'App',
  components: {
    
  },
  data (){
    return {
      followers: 0,
      user: {
        id: 1,
        username: "_UncleCycha_",
        firstName: "Sicelo",
        lastName: "Sitsha",
        email: "sicelositsha@yahoo.com",
        isAdmin: true
      }
    }
  },
  computed: {
    fullName() {
      return `${this.user.firstName} ${this.user.lastName}`;
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
