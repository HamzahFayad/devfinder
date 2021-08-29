<template>
  <div id="search">
    <input
      type="text"
      placeholder="Search Github username..."
      v-model="username"
      @keydown.enter="search()"
    />

    <div class="userCard" v-if="userInfos">
      <img :src="userInfos.avatar_url" alt="" />
      <p>Name: {{ userInfos.login }}</p>
      <p>Bio: {{ userInfos.bio }}</p>
      <p>Joined: {{ userInfos.created_at }}</p>
      <a :href="userInfos.html_url">@{{ userInfos.login }}</a>
      <br />
      <p>Repos: {{ userInfos.public_repos }}</p>
      <p>Followers: {{ userInfos.followers }}</p>
      <p>Following: {{ userInfos.following }}</p>
      <br />

      <p>Location: {{ userInfos.location }}</p>
      <a :href="userInfos.blog">Blog: {{ userInfos.blog }}</a>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  components: {},
  data() {
    return {
      username: "",
      userInfos: "",
    };
  },
  methods: {
    search() {
      axios
        .get("https://api.github.com/users/" + this.username)
        .then((res) => {
          console.log(res.data);
          this.userInfos = res.data;
        })
        .catch((err) => console.log(err));
    },
  },
};
</script>

<style lang="scss">
input {
  border: none;
  box-shadow: 1px 3px 9px #1c1c1c8c;
  outline: none;
  color: var(--text-color);
  width: 800px;
  height: 50px;
  border-radius: 8px;
  padding: 0 6px;
  margin-top: 25px;
  background-color: var(--cards-color);
}
input::placeholder {
  color: var(--text-color);
  //padding: 0 12px;
}
.userCard {
  margin-top: 25px;
  box-shadow: 1px 3px 9px #1c1c1c8c;
  background: var(--cards-color);
  width: 800px;
  border-radius: 8px;
  padding: 20px 6px;
  display: block;
  margin: 25px auto;
  img {
    border-radius: 50%;
    max-width: 150px;
    height: 150px;
  }
}
a {
  text-decoration: none;
  font-weight: 600;
  color: var(--text-color);
}

@media only screen and (max-width: 825px) {
  input,
  .userCard {
    width: 350px;
  }
}
</style>