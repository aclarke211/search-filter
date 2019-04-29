<template>
  <div :class="className">
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
  name: 'SelectFilter',

  props: {
    /**
    * The original data that will be filterd by the component
    */
    dataToFilter: {
      type: Array,
      default: () => ([
        {
          username: 'jhbjkbjh@test.com',
          role: 'Admin',
          fascias: ['JDSPORTS', 'JDSPORTS_BE'],
          services: ['content_editor'],
        },
        {
          username: 'bjhiiujb@test.com',
          role: 'User',
          fascias: ['JDSPORTS'],
          services: ['content_editor', 'email_builder'],
        },
        {
          username: 'opjjbvghc@test.com',
          role: 'Admin',
          fascias: ['JDSPORTS_BE'],
          services: ['content_editor'],
        },
        {
          username: 'dfxgvbbhj@test.com',
          role: 'User',
          fascias: ['JDSPORTS'],
          services: ['email_builder'],
        },
      ]),
    },

    /**
    * The select boxes used to filter the data
    */
    selectFilters: {
      type: Array,
      default: () => ([
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
            {
              text: 'User',
              value: 'user',
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
      ]),
    },
  },

  data: () => ({
    className: 'select-filter',
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
      let filteredArray = this.dataToFilter;

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

          return false;
        });
      }
      return array;
    },
  },

  searchFilter() {
    // return this.search ? this.items.filter(item => {
    //     let match = false
    //     for (let key in item) {
    //       console.log(item[key]);
    //       if (item[key].toLowerCase().includes(this.search.toLowerCase())) {
    //         return true
    //       }
    //     }
    //   })
    //   : this.items
  },
};
</script>

<style lang="scss">
.select-filter {
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
}
</style>
