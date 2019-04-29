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
      <pre class="filtered-data__json data-json">{{ this.filteredData }}</pre>

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
        fascias: ['JDSPORTS', 'JDSPORTS_BE'],
        services: ['content_editor'],
      },
      {
        role: 'User',
        fascias: ['JDSPORTS'],
        services: ['content_editor', 'email_builder'],
      },
      {
        role: 'Admin',
        fascias: ['JDSPORTS_BE'],
        services: ['content_editor'],
      },
      {
        role: 'User',
        fascias: ['JDSPORTS'],
        services: ['email_builder'],
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
        label: 'Service',
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
    selectedRole() {
      return this.getSelectedValue('Role');
    },

    selectedFascia() {
      return this.getSelectedValue('Fascia');
    },

    selectedService() {
      return this.getSelectedValue('Service');
    },

    filteredData() {
      let filteredArray = this.items;

      filteredArray = this.filterByValue('role', this.selectedRole, filteredArray);
      filteredArray = this.filterByValue('fascias', this.selectedFascia, filteredArray);
      filteredArray = this.filterByValue('services', this.selectedService, filteredArray);

      return filteredArray;
    },
  },

  methods: {
    getSelectedValue(value) {
      const toReturn = this.selectFilters.filter(selectData => selectData.label === value);

      return toReturn[0].current;
    },

    filterByValue(key, currentValue, arrayToFilter) {
      let array = arrayToFilter;
      if (currentValue !== '') {
        array = arrayToFilter.filter((item) => {
          if (Array.isArray(item[key])) {
            let checkSubArray = false;

            item[key].forEach((singleValue) => {
              if (singleValue.toLowerCase() === currentValue.toLowerCase()) {
                checkSubArray = true;
                return true;
              }
              return false;
            });
            if (checkSubArray) {
              return item[key];
            }
          } else {
            return item[key].toLowerCase() === currentValue.toLowerCase();
          }
        });
      }
      return array;
    },
  },
};
</script>

<style lang="scss">
  .data {
    margin: 1rem 0;

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
        margin: .25rem 1rem;
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
