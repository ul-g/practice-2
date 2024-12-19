<template>
  <div class="ui card">
    <div class="image">
      <img :src="user.avatar_url" alt="User Avatar" />
    </div>
    <div class="content">
      <a class="header" :href="user.html_url" target="_blank">{{ user.name || 'No Name' }}</a>
      <div class="meta">
        <span class="date">Joined {{ formattedJoinDate }}</span>
      </div>
      <div class="description">
        <p>{{ user.bio || 'No bio available.' }}</p>
      </div>
    </div>
    <div class="extra content">
      <a>
        <i class="users icon"></i>
        {{ user.followers }} Followers
      </a>
    </div>
  </div>
</template>

<script>
export default {
  name: 'GitHubProfile',
  data() {
    return {
      user: {},
    };
  },
  props: {
    username: {
      type: String,
      required: true,
    },
  },
  computed: {
    formattedJoinDate() {
      if (!this.user.created_at) return '';
      const date = new Date(this.user.created_at);
      return date.toLocaleDateString();
    },
  },
  methods: {
    async fetchUserData() {
      try {
        const response = await fetch(`https://api.github.com/users/${this.username}`);
        if (response.ok) {
          this.user = await response.json();
        } else {
          console.error('Error fetching GitHub data');
        }
      } catch (error) {
        console.error('Fetch error: ', error);
      }
    },
  },
  watch: {
    username() {
      this.fetchUserData();
    },
  },
  mounted() {
    this.fetchUserData();
  },
};
</script>

<style scoped>
.card {
  width: 300px;
  margin: 20px auto;
}
</style>
