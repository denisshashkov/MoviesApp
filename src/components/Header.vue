<template>
  <header class="header">
    <b-navbar type="dark" class="navbar" variant="dark">
      <b-container>
        <b-navbar-brand href="/?">MovieDB</b-navbar-brand>
        <b-nav-form>
          <b-form-input
            class="mr-sm-2 search-input"
            placeholder="Search"
            debounce="500"
            v-model="searchValue"
          ></b-form-input>
        </b-nav-form>
      </b-container>
    </b-navbar>
  </header>
</template>

<script>
import { mapActions } from "vuex";
export default {
  name: "Header",
  data: () => ({
    searchValue: "",
  }),
  watch: {
    searchValue: "onSearchValueChanged",
  },
  methods: {
    ...mapActions("movies", [
      "searchMovies",
      "fetchMovies",
      "toggleSearchState",
    ]),
    onSearchValueChanged(val) {
      if (val) {
        this.searchMovies(val);
        this.toggleSearchState(true);
      } else {
        this.fetchMovies();
        this.toggleSearchState(false);
      }
    },
  },
};
</script>

<style scoped>
.header {
  background-image: linear-gradient(45deg, #9a0204 0%, #200208 50%);
  position: fixed;
  top: 0;
  left: 0;
  z-index: 100;
  right: 0;
}

.navbar {
  background-color: rgba(0, 0, 0, 0.5) !important;
}

.search-input {
  color: #000;
  background: #ccc;
  border-color: rgba(0, 0, 0, 0.6);
}

.search-input:focus {
  box-shadow: none;
  background: rgba(255, 255, 255, 0.9);
  border-color: rgba(0, 0, 0, 0.6);
}

.form-inline {
  display: block;
}
</style>
