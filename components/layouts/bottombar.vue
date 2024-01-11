<template>
    <div class="container mx-auto w-full">
      <div class="fixed bottom-0 md:hidden mx-auto z-50 w-full -translate-x-1/2 bg-white border-t border-gray-200 left-1/2 dark:bg-gray-700 dark:border-gray-600">
        <div class="grid h-full max-w-lg grid-cols-5 mx-auto">
          <router-link to="/">
            <button
              data-tooltip-target="tooltip-home"
              @click="handleNavigation('/')"
              type="button"
              class="inline-flex flex-col items-center justify-center p-4 hover:bg-gray-50 dark:hover:bg-gray-800 group"
            >
              <svg
                class="w-5 h-5 mb-1 text-gray-500 dark:text-gray-400 group-hover:text-blue-600 dark:group-hover:text-blue-500"
                aria-hidden="true"
                xmlns="http://www.w3.org/2000/svg"
                fill="currentColor"
                viewBox="0 0 20 20"
              >
                <path d="M19.707 9.293l-2-2-7-7a1 1 0 0 0-1.414 0l-7 7-2 2a1 1 0 0 0 1.414 1.414L2 10.414V18a2 2 0 0 0 2 2h3a1 1 0 0 0 1-1v-4a1 1 0 0 1 1-1h2a1 1 0 0 1 1 1v4a1 1 0 0 0 1 1h3a2 2 0 0 0 2-2v-7.586l.293.293a1 1 0 0 0 1.414-1.414Z" />
              </svg>
              <span class="sr-only">Home</span>
            </button>
          </router-link>
          <!-- ... (similar changes for other buttons) ... -->
        </div>
      </div>
      <div v-if="search" class="w-[100%] h-[88vh] bg-white z-40 fixed bottom-0 left-0">
        <!-- ... (similar changes for the search bar) ... -->
      </div>
    </div>
  </template>
  
  <script>
  import { IoIosSearch } from "vue-ionicons";
  
  export default {
    data() {
      return {
        search: false,
        data: [],
        textSearch: "",
        searchResult: null,
        API: "https://fakestoreapi.com/products"
      };
    },
    mounted() {
      this.fetchData();
    },
    methods: {
      fetchData() {
        axios
          .get(this.API)
          .then((res) => (this.data = res.data))
          .catch((err) => console.log(err));
      },
      handleSearch(value) {
        this.textSearch = value;
        if (!value.length) {
          this.searchResult = null;
        } else {
          this.searchResult = this.data.filter((item) =>
            item.title.toLowerCase().includes(value.toLowerCase())
          );
        }
      },
      handleNavigation(route) {
        this.$router.push(route);
      }
    },
    components: {
      IonIcon: IonIcon
    }
  };
  </script>
  
  <style scoped>
  /* Add your component-specific styles here */
  </style>
  