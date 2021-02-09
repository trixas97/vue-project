<template>
 <div class="user-profile">
   <div class="user-profile_sidebar">
     <div class="user-profile_user-panel">
         <h1 class="user-profile_username">@{{ user.username }}</h1>
         <div class="user-profile_admin-badge" v-if="user.isAdmin">
             Admin
         </div>
         <div class="user-profile_follower-count">
             <strong>Followers: </strong>{{followers}}
         </div>
      </div>
      <CreateTwootPanel @add-twoot="addTwoot"/>
   </div>
     <div class="user-profile_twoots-wrapper">
         <TwootItem 
            v-for="twoot in  user.twoots" 
            :key="twoot.id" 
            :username="user.username" 
            :twoot="twoot"
        />
     </div>
<!--     
  @{{ user.username }} - {{ fullName }}
  
  <button @click="followUser">
    Follow
  </button> -->
 </div>
</template>

<script>
import TwootItem from "./TwootItem";
import CreateTwootPanel from "../components/CreateTwootPanel";

export default {
  name: 'UserProfile',
  components: { CreateTwootPanel, TwootItem },
  data () {
    return {
      followers: 0,
      user: {
        id: 1,
        username: '_Trixas97',
        firstname: 'Mike',
        lastname: 'Trixas',
        email: 'trixasmixas@gmail.com',
        isAdmin: true,
        twoots: [
            {id: 1, content: 'First twoot'},
            {id: 2, content: 'Second twoot'}
        ]
      }
    }
  },
  computed: {
    fullName() {
      return `${this.user.firstname} ${this.user.lastname}`
    },

    newTwootCharacterCount() {
      return this.newTwootContent.length;
    }
  },
  methods: {
    followUser(){
      this.followers++
    },
    
    addTwoot(twoot){
      this.user.twoots.unshift({id: this.user.twoots.length + 1, content: twoot});
    }
  },
  mounted() {
    this.followUser();
  }
}
</script>

<style lang='scss' scoped>
    .user-profile {
        display: grid;
        grid-template-columns: 1fr 3fr;
        grid-gap: 50px;
        width: 1fr;
        padding: 50px 5%;

        .user-profile_user-panel {
            display: flex;
            flex-direction: column;
            // margin-right: 50px;
            padding: 20px;
            background-color: #fff;
            border-radius: 5px;
            border: 1px solid #dfe3e8;
            margin-bottom: auto;

            h1 {
                margin: 0;
            }

            .user-profile_admin-badge {
              background-color: rebeccapurple;
              color: white;
              border-radius: 5px;
              margin-right: auto;
              padding: 0 10px;
              font-weight: bold;
            }

        }

        .user-profile_twoots-wrapper {
          display: grid;
          grid-gap: 10px;
          margin-bottom: auto;
        }
    }
    
</style>
