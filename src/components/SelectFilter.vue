<template>
  <div :class="className">
      <div
        v-if="filters"
        class="filters">
        <div
          v-for="(selectFilter, selectKey) in filters"
          :key="selectKey"
          class="select__container">
            <label :for="`select-filter-${selectKey}`">{{ selectFilter.label }}</label>
            <select
            class="select-box"
            :id="`select-filter-${selectKey}`"
            v-model="selectFilter.current">
              <option
                v-for="(singleOption, optionKey) in selectFilter.options"
                :key="optionKey"
                v-bind:value="singleOption.value"
                class="'select-option'"
                :id="`select-option-${optionKey}`">
                  {{ singleOption.text }}
              </option>
            </select>
          </div>
      </div>

    <div
    v-if="showFilteredData"
    class="filtered-data">
      <pre
      v-if="this.filteredData.length >= 1"
      class="filtered-data__json">{{ this.filteredData }}</pre>
      <p
        v-else
        class="filter-data__empty-message">{{ this.emptyMessage }}</p>
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
          filterValue: 'role',
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
          filterValue: 'fascias',
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
          filterValue: 'services',
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

    /**
    * The message which appears if no data matches the filter criteria
    */
    emptyMessage: {
      type: String,
      default: 'There are no results for the chosen filters.',
    },

    /**
    * Toggle to show/hide the filtered data
    */
    showFilteredData: {
      type: Boolean,
      default: true,
    },
  },

  data: () => ({
    className: 'select-filter',
  }),

  computed: {
    filters() {
      return this.selectFilters;
    },

    filteredData() {
      let filteredArray = this.dataToFilter;

      this.filters.forEach((filter) => {
        filteredArray = this.filterByValue(filter.filterValue,
          this.getSelectedValue(filter.label), filteredArray);
      });
      return filteredArray;
    },
  },

  methods: {
    getSelectedValue(value) {
      const toReturn = this.filters.filter(selectData => selectData.label === value);

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

    /*
    * NEED TO IMPLEMENT A SEARCH BOX FITLER
    */

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
  max-width: 100%;

  .filters {
    align-items: center;
    display: flex;
    flex-flow: column wrap;
    justify-content: center;
    transition: all .5s;

    @media only screen and (min-width: 767px) {
      flex-direction: row;
    }

    .select__container {
      align-items: center;
      display: flex;
      flex-flow: column wrap;
      justify-content: center;
      margin: 1rem 0;
      padding: .5rem;
      max-width: 100%;
      transition: all .5s;

      @media only screen and (min-width: 767px) {
        margin: 1rem;
        width: unset;
      }

      label {
        flex: 1;
        font-size: 1rem;
        font-weight: 600;
      }

      .select-box {
        border-radius: 20rem;
        font-size: .9rem;
        margin: .75rem;
        max-width: 100%;
        padding: .75rem 2rem;
        width: 15rem;

        @media only screen and (min-width: 767px) {
          margin: 1rem 2rem;
        }
      }
    }
  }

  .filtered-data {
    margin: 1rem 0;
    display: flex;
    align-items: center;
    justify-content: center;

    &__json {
      font-size: .8rem;
    }
  }
}
</style>
