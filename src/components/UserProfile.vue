<template>
 <div class="user-profile">
     <div class="user-profile_user-panel">
         <h1 class="user-profile_username">@{{ user.username }}</h1>
         <div class="user-profile_admin-badge" v-if="user.isAdmin">
             Admin
         </div>
         <div class="user-profile_follower-count">
             <strong>Followers: </strong>{{followers}}
         </div>
         <form class="user-profile_create-twoot" @submit.prevent="createNewTwoot" :class="{'--exceeded': newTwootCharacterCount > 180}">
           <label for="newTwoot"><strong>New Twoot</strong> ({{newTwootCharacterCount}}/180) </label>
           <textarea id="newTwoot" rows="4" v-model="newTwootContent"/>

           <div class="user-profile_create-twoot-type">
             <label for="newTwootType"><strong>Type: </strong></label>
             <select id="newTwootType" v-model="selectedTwootType">
               <option :value="option.value" v-for="(option, index) in twootTypes" :key="index">
                 {{ option.name }}
               </option>
             </select>
           </div>

           <button>Twoot!</button>
         </form>
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
import TwootItem from "./TwootItem"

export default {
  name: 'UserProfile',
  components: { TwootItem },
  data () {
    return {
      newTwootContent: '',
      selectedTwootType: 'instant',
      twootTypes: [
        {value: 'draft', name: 'Draft'},
        {value: 'instant', name: 'Instant Twoot'}
      ],
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
    createNewTwoot(){

      if (this.newTwootContent && this.selectedTwootType !== 'draft'){
        this.user.twoots.unshift({ 
          id: this.user.twoots.length + 1,
          content: this.newTwootContent
        })
        this.newTwootContent = '';
      }
      
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
        /* grid-gap: 50px; */
        width: 100%;
        padding: 50px 5%;

        .user-profile_user-panel {
            display: flex;
            flex-direction: column;
            margin-right: 50px;
            padding: 20px;
            background-color: #fff;
            border-radius: 5px;
            border: 1px solid #dfe3e8;
            /* margin-bottom: auto; */

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

            .user-profile_create-twoot {
              display: flex;
              padding-top: 20px;
              flex-direction: column;

              &.--exceeded {
                color: red;
                border-color: red;
              }
            }
        }

        .user-profile_twoots-wrapper {
          display: grid;
          grid-gap: 10px;
          margin-bottom: auto;
        }
    }
    
</style>
