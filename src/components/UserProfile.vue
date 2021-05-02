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
    </div>
    <div class="user-profile_twoots-wrapper">
        <TwootItem v-for="twoot in user.twoots" :key="twoot.id" :username="user.username" :twoot="twoot" @favorite="toggleFavorite" />
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
                {id: 3, content: "This is the third twoot"}
            ]
        },
    };
  },
  computed: {
    fullName() {
      return `${this.user.firstName} ${this.user.lastName}`;
    },
  },
  methods: {
    followUser() {
      this.followers++;
    },
    toggleFavorite(id){
        console.log(`Favorited twoot #${id}`);
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
}

.user-profile_admin-badge {
    background: purple;
    color: white;
    border-radius: 5px;
    margin-right : auto;
    padding: 0 10px;
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
</style>
