<template>
  <div id="app">
    <header class="app-header">
      <h1 class="text--primary">{{$route.meta.pageName}}</h1>
    </header>
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App',
};
</script>

<style lang="scss">
  .app-header {
    margin: 0;
    height: 72px;
    padding-top: 24px;
    background: rgba(255, 255, 0, .2);

    > h1 {
      margin: 0;
      text-shadow: 0 2px 0 rgba(#170A71, 0.15);
      text-align: center;
      letter-spacing: 2px;
      font-size: 28px;
    }
  }
</style>
