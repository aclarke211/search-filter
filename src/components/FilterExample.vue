<template>
  <div class="filter__outer">
    <div class="default-data data">
      <h2 class="default-data__title data-title">Default Data</h2>
      <p class="default-data__json data-json">{{ this.items }}</p>
    </div>

    <div class="filters">
      <h2 class="filters__title data-title">Filters</h2>
      <div class="select-filters">
        <div
          v-for="(selectFilter, selectKey) in selectFilters"
          :key="selectKey"
          class="select__container">
            <h3>{{ selectFilter.label }}</h3>

            <select
            class="select-box"
            v-model="selectFilter.current">
              <option
                v-for="(singleOption, optionKey) in selectFilter.options"
                :key="optionKey"
                v-bind:value="singleOption.value"
                :class="['select-option', `select-option-${optionKey}`]">
                  {{ singleOption.text }}
              </option>
            </select>

          </div>
      </div>
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

    selectFilters: [
      {
        label: 'Role',
        current: '',
        options: [
          {
            text: 'All',
            value: '',
          },
          {
            text: 'Admin',
            value: 'admin',
          },
        ],
      },
      {
        label: 'Fascia',
        current: '',
        options: [
          {
            text: 'All',
            value: '',
          },
          {
            text: 'JD Sports (GB)',
            value: 'JDSPORTS',
          },
          {
            text: 'JD Sports (BE)',
            value: 'JDSPORTS_BE',
          },
        ],
      },
      {
        label: 'Services',
        current: '',
        options: [
          {
            text: 'All',
            value: '',
          },
          {
            text: 'Content Editor',
            value: 'content_editor',
          },
          {
            text: 'Email Builder',
            value: 'email_builder',
          },
        ],
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

  .filters {
    .select-filters {
      display: flex;

      .select__container {
        margin: 1rem;
        display: flex;
        align-items: center;
        justify-content: center;

        .select-box {
          margin: .5rem;
        }
      }
    }
  }
</style>
