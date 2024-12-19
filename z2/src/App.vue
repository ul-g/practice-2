<template>
  <div id="app">
    <h1>GitHub Profile Viewer</h1>
    <GitHubProfile :username="'octocat'" />
  </div>
</template>

<script>
import GitHubProfile from './components/GitHubProfile.vue';

export default {
  name: 'App',
  components: {
    GitHubProfile
  }
};
</script>

<style>
#app {
  text-align: center;
  padding: 20px;
}
</style>
