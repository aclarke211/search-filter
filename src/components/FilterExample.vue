<template>
  <div class="filter__outer">
    <div class="default-data data">
      <h2 class="default-data__title data-title">Default Data</h2>
      <p class="default-data__json data-json">{{ this.items }}</p>
    </div>

    <div class="filters">
      <h2 class="filters__title data-title">Filters</h2>
    </div>

    <div class="filtered-data data">
      <h2 class="filter-data__title data-title">Filtered Data</h2>
      <p class="filtered-data__json data-json">{{ this.filteredData }}</p>

    </div>
  </div>
</template>

<script>
export default {
  name: 'FilterExample',

  data: () => ({
    items: [
      {
        role: 'Admin',
        fascia: 'JDSPORTS',
        services: ['Content Editor'],
      },
      {
        role: 'User',
        fascia: 'JDSPORTS',
        services: ['Content Editor'],
      },
      {
        role: 'Admin',
        fascia: 'JDSPORTS_BE',
        services: ['Content Editor'],
      },
      {
        role: 'User',
        fascia: 'JDSPORTS',
        services: ['Email Builder'],
      },
    ],
  }),

  computed: {
    filteredData() {
      return this.items;
    },
  },
};
</script>

<style lang="scss">
  .data {
    margin: 3rem 0;

    &-title {
      border-bottom: 2px solid slategrey;
      display: inline-flex;
      padding: 0 .25rem .25rem;
    }

    &-json {
      font-size: .8rem;
    }
  }
</style>
