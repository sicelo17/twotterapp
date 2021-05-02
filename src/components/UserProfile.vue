<template>
  <div class="user-profile">
    <div class="user-profile_user-panel">
      <h1 class="user-profile_username">
        @{{ user.username }}
      </h1>
      <div class="user-profile_admin-badge" v-if="user.isAdmin">
          Admin
      </div>
      <div class="user-profile_followerCount">
        <strong>Followers: </strong>{{ followers }}
      </div>
      <form class="user-profile_create-twoot" @submit.prevent="createNewTwoot" :class="{'--exceeded': newTwootCharacterCount > 180}">
          <label for="newTwoot"><strong>New Twoot</strong>({{ newTwootCharacterCount }}/180)</label>
          <textarea id="newTwoot" rows="4" v-model="newTwootContent "></textarea>

          <div class="user-profile_create-twoot-type">
              <label for="newTwootType"><strong>Type: </strong></label>
              <select id="newTwootType" v-model="selectedTwootType">
                  <option :value="option.value" v-for="(option, index) in twootTypes" :key="index">
                      {{option.name}}
                  </option>
              </select>
          </div>

          <button>
              Twoot
          </button>
      </form>
    </div>
    <div class="user-profile_twoots-wrapper">
        <TwootItem 
        v-for="twoot in user.twoots" 
        :key="twoot.id" 
        :username="user.username" 
        :twoot="twoot"
        @favorite="toggleFavorite" />
    </div>
  </div>
</template>

<script>

import TwootItem from './TwootItem';
export default {
  name: "UserProfile",
  components: {
      TwootItem
  },
  data() {
    return {
        newTwootContent: '',
        selectedTwootType: 'instant',
        twootTypes : [
            {value: 'draft', name: 'Draft'},
            {value: 'instant', name: 'Instant Twoot'}
        ],
        followers: 0,
        user: {
            id: 1,
            username: "_UncleCycha_",
            firstName: "Sicelo",
            lastName: "Sitsha",
            email: "sicelositsha@yahoo.com",
            isAdmin: true,
            twoots: [
                {id: 1, content: "Twooter is amazing "},
                {id: 2, content: "Vuejs is fun"},

            ]
        },
    };
  },
  computed: {
    newTwootCharacterCount() {
        return this.newTwootContent.length;
    }
  },
  methods: {
    followUser() {
      this.followers++;
    },
    toggleFavorite(id){
        console.log(`Favorited twoot #${id}`);
    },
    createNewTwoot() {
        if(this.newTwootContent && this.selectedTwootType !== 'draft'){
            this.user.twoots.unshift({
                id: this.user.twoots.length + 1,
                content: this.newTwootContent
            });

            this.newTwootContent = '';
        }
    }
  },
  mounted() {
    this.followUser();
  },
};
</script>

<style scoped>
.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  width: 100%;
  padding: 50px 10px;
}

.user-profile_user-panel {
    display: flex;
    flex-direction: column;
    margin-right: 50px;
    padding: 20px;
    background-color: white;
    border-radius: 5px;
    border: 1px solid #DFE3E8;
    height: 35vh;
}

.user-profile_admin-badge {
    background: purple;
    color: white;
    border-radius: 5px;
    margin-right : auto;
    padding: 0 10px;
    font-weight: bold;
}

.user-profile_followerCount {
    margin: 0;
    padding: 0;
}

h1 {
    margin: 0;
}

.user-profile_twoots-wrapper {
    display: grid;
    grid-gap: 10px;
}

.user-profile_create-twoot {
    border-top: 1px solid #DFE3E8;
    padding-top: 20px;
    display: flex;
    flex-direction: column;
}

.--exceeded {
    border: red;
    color: red;
}
</style>
