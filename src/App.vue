<template>
  <div id="app">
    <h1 class="title">Select Filter</h1>
    <SelectFilter :dataToFilter="selectFilterData" />
  </div>
</template>

<script>
import SelectFilter from '@/components/SelectFilter.vue';

export default {
  name: 'app',

  components: {
    SelectFilter,
  },

  data: () => ({
    selectFilterData: [
      {
        username: 'qcfwj@test.com',
        role: 'Admin',
        fascias: ['JDSPORTS', 'JDSPORTS_BE'],
        services: ['content_editor'],
      },
      {
        username: 'njbjkbkjedk@test.com',
        role: 'User',
        fascias: ['JDSPORTS'],
        services: ['content_editor', 'email_builder'],
      },
      {
        username: 'oifwmnvin@test.com',
        role: 'Admin',
        fascias: ['JDSPORTS_BE'],
        services: ['content_editor'],
      },
      {
        username: 'ydfmkvbdflkj@test.com',
        role: 'User',
        fascias: ['JDSPORTS'],
        services: ['email_builder'],
      },
    ]
  }),
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
