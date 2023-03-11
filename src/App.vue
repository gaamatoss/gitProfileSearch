<script>
export default {
  data() {
    return {
      gitUserName: "",
      profile: {},
      repos: {},
    };
  },
  methods: {
    getGitInfo(username) {
      fetch(`https://api.github.com/users/${username}`)
        .then((res) => res.json())
        .then((data) => {
          this.profile = data;
        });
      fetch(`https://api.github.com/users/${username}/repos`)
        .then((res) => res.json())
        .then((data) => {
          this.repos = data;
          console.log(data);
        });
    },
  },
};
</script>

<template>
  <div class="search-section">
    <input
      type="text"
      class="search-input"
      placeholder="Search by User Name"
      v-model="gitUserName"
      @keypress.enter="getGitInfo(gitUserName)"
    />
    <button class="search-button" @click="getGitInfo(gitUserName)">
      Search
    </button>
  </div>
  <div class="profileInfo-section">
    <div class="profile-header">
      <img class="profile-avatar" :src="profile.avatar_url" alt="" />
      <section class="cardInfo-section">
        <h4>Login: <br />{{ profile.login }}</h4>
        <h4>Name: <br />{{ profile.name }}</h4>
        <h4>Blog: <br />{{ profile.blog }}</h4>
        <h4>Company: <br />{{ profile.company }}</h4>
        <h4>Location: <br />{{ profile.location }}</h4>
        <h4>Bio: <br />{{ profile.bio }}</h4>
        <h4>
          Following:<br />
          {{ profile.following }}
        </h4>
        <h4>
          Followers:<br />
          {{ profile.followers }}
        </h4>
      </section>
    </div>
    <div class="repos-section">
      <ul>
        <li v-for="item in repos" :key="item.id" class="repo-item">
          {{ item.name }}
          <a :href="item.html_url" target="_blank" style="cursor: pointer"
            ><button class="visitRepo-btn">Visit Repo</button></a
          >
        </li>
      </ul>
    </div>
  </div>
</template>
