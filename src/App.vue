<template>
  <div id="app">
    <h1 class="title">Filter / Search</h1>
    <SelectFilter />
  </div>
</template>

<script>
import SelectFilter from '@/components/SelectFilter.vue';

export default {
  name: 'app',

  components: {
    SelectFilter,
  },
};
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

.title {
  text-align: center;
}
</style>
