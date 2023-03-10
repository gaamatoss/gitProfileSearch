<script>
export default {
  data() {
    return {
      gitUserName: "",
      profile: {},
    };
  },
  methods: {
    getGitProfile(username) {
      fetch(`https://api.github.com/users/${username}`)
        .then((res) => res.json())
        .then((data) => {
          this.profile = data;
        });
    },
  },
};
</script>

<template>
  <input type="text" placeholder="Search Profile" v-model="gitUserName" />
  <button @click="getGitProfile(gitUserName)">Search</button>
  <div>
    <ul>
      <li v-for="(item, key) in profile">{{ key }}: {{ item }}</li>
    </ul>
  </div>
</template>
