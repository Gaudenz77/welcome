<template>
    <div class="container">
      <div class="row justify-content-center bg-info">
        <div class="col-sm-4 mt-5 p-5">
          <form @submit.prevent="applyFilter">
            <label>Filter by Category:</label><br>
            <label for="food" class="form-check-label">Food</label>
            <input type="checkbox" class="form-check-input mt-0" v-model="filter.food" name="category" id="food">
            <label for="education" class="form-check-label">Education</label>
            <input type="checkbox" class="form-check-input mt-0" v-model="filter.education" name="category" id="education">
            <label for="general" class="form-check-label">General</label>
            <input type="checkbox" class="form-check-input mt-0" v-model="filter.general" name="category" id="general">
            <br>
            <!-- <label>Filter by Keyword:</label>
            <input class="btn-group" role="group" aria-label="Basic mixed styles example" type="text" v-model="searchText" name="keyword"> -->
            <button type="submit" class="btn btn-warning">Apply Filter</button>
            <button type="button"  class="btn btn-success" @click="resetFilter">Reset Filters</button>
          </form>
        </div>
      </div>
    </div>
</template>

<script>
export default {
  data() {
    return {
      filter: {
      food: false,
      education: false,
      general: false,
    },
    /* searchText: "",*/
  }; 
  },
  methods: {
    applyFilter() {
      console.log('Applying filter...');
      console.log('Filter:', this.filter);
      /* console.log('Search text:', this.searchText); */
      // Emit an event to notify the parent component
      // that the filter has been applied
      this.$emit("filter-applied", {
        filter: {
          food: this.filter.food,
          education: this.filter.education,
          general: this.filter.general,
        },
        /* searchText: this.searchText,*/
      } );
    },
    resetFilter() {
      // Reset the filter data
      this.filter.food = false;
      this.filter.education = false;
      this.filter.general = false;
      /* this.searchText = ""; */
      // Emit an event to notify the parent component
      // that the filter has been reset
      this.$emit("filter-reset");
    },
  },
};
</script>



<style scope>

</style>