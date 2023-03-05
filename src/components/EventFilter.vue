<!-- <template>
    <div class="container">
      <div class="row justify-content-center bg-info">
        <div class="col-sm-4 mt-5 p-5">
          <form @submit.prevent="applyFilter">
            <label>Filter by Category:</label>
            <input type="checkbox" class="form-check-input mt-0" v-model="filter.food" name="category" id="food">
            <label for="food" class="form-check-label">Food</label>
            <input type="checkbox" class="form-check-input mt-0" v-model="filter.education" name="category" id="education">
            <label for="education" class="form-check-label">Education</label>
            <input type="checkbox" class="form-check-input mt-0" v-model="filter.general" name="category" id="general">
            <label for="general" class="form-check-label">General</label>
            <br>
            <label>Filter by Keyword:</label>
            <input class="btn-group" role="group" aria-label="Basic mixed styles example" type="text" v-model="keywordFilter" name="keyword">
            <br>
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
      },
      searchText: "",
    };
  },
  methods: {
    applyFilter() {
      // Emit an event to notify the parent component
      // that the filter has been applied
      this.$emit("filter-applied", {
        category: {
          food: this.filter.food,
          education: this.filter.education,
        },
        searchText: this.searchText,
      });
    },
    resetFilter() {
      // Reset the filter data
      this.filter.food = false;
      this.filter.education = false;
      this.searchText = "";
      // Emit an event to notify the parent component
      // that the filter has been reset
      this.$emit("filter-reset");
    },
  },
};
</script>



<style scope>

</style> -->