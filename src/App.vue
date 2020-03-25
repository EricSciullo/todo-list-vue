<template>
  <div>
    <a class="home" href="https://sciullo.dev/">
      <div id="profile_img" style="background: url(https://avatars0.githubusercontent.com/u/35748671?v=4) center;"></div>
    </a>
    <a class="github" href="https://github.com/EricSciullo/todo-list-vue">
      <span class="fa fa-github"></span>
    </a>
    <Todos />
  </div>
</template>

<script>
import Todos from './components/Todos.vue';

export default {
  name: 'App',
  components: {
    Todos,
  },
};
</script>

<style>
#profile_img {
  width: 60px;
  height: 60px;
  min-width: 60px;
  min-height: 60px;
  max-width: 60px;
  max-height: 60px;
  border-radius: 50%;
  background-size: cover !important;
  background-repeat: no-repeat !important;
  margin-top: 10px;
  margin-left: 10px;
}

.home {
  float: left;
}

.github {
  font-size: 72px;
  line-height: 1;
  padding-left: 10px;
}
</style>
