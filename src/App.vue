<template>
 <div id="app">
   <nav>
     <div class="navigation_logo">
       Twotter
     </div>
     <div class="navigation_user">
       {{ user.username }}
     </div>
   </nav>
   <UserProfile/>
 </div>
</template>

<script>

import UserProfile from './components/UserProfile.vue'

export default {
  name: 'App',
  components: { UserProfile },
  data() {
    return {
      user: {
        username: '_trixas97'
      }
    }
  }
}
</script>

<style lang="scss">
    #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
    display: flex;
    flex-direction: column;
    min-height: 100vh;

    nav {
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 15px 5%;
      box-shadow: 0 4px 5px 0 rgba(0, 0, 0, 0.2),
        0 6px 20px 0 rgba(0, 0, 0, 0.19);
      background-color: teal;
      color: white;
      .navigation_logo {
        font-weight: bold;
        font-size: 24px;
      }
      .navigation_user {
        font-weight: bold;
      }
    }
  }
</style>
