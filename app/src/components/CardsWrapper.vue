<template>
  <div>
    <CardsFilter
      :filters="filters"
      @filter-selected="updateSelectedFilter"
      @sort-order-changed="updateSortOrder"
    />
    <div class="wrapper">
      <CardItem
        v-for="card in filteredItems"
        :image="card.images[0].src"
        :name="card.name"
        :description="card.short_description"
        :category="card.categories"
        :key="card.name"
      />
    </div>
    <div class="spinner-border text-primary" role="status"></div>
    <ScrollToTop />
  </div>
</template>

<script>
import CardItem from "./CardItem.vue";
import CardsFilter from "./CardsFilter.vue";
import ScrollToTop from "./ScrollToTop.vue";

export default {
  components: {
    CardItem,
    CardsFilter,
    ScrollToTop,
  },
  data() {
    return {
      items: [],
      filteredItems: [],
      filters: [],
      selectedFilter: "all",
      sortCriteria: "default",
      sortOrder: "default",
      page: 1,
    };
  },
  mounted() {
    this.loadData();
    window.addEventListener("scroll", this.handleScroll);
  },
  methods: {
    loadData() {
      window.receiveData = (data) => {
        this.items = this.items.concat(data);
        this.page += 1;
        this.updateFilters();
        this.filterItems();
      };

      const script = document.createElement("script");
      script.src = `https://greet.bg/wp-json/wc/store/products?page=${
        this.page
      }${this.sortCriteria === "default" ? "" : this.sortCriteria}${
        this.sortOrder === "default" ? "" : this.sortOrder
      }&_jsonp=receiveData`;
      document.body.appendChild(script);
    },
    handleScroll() {
      const scrollHeight = document.documentElement.scrollHeight;
      const scrollTop = document.documentElement.scrollTop;
      const clientHeight = document.documentElement.clientHeight;

      if (scrollTop + clientHeight >= scrollHeight) {
        this.page += 1;
        this.loadData();
      }
    },
    updateFilters() {
      const uniqueCategories = this.items.reduce((categories, item) => {
        item.categories.forEach((category) => {
          if (!categories.some((c) => c.id === category.id)) {
            categories.push({ id: category.id, name: category.name });
          }
        });
        return categories;
      }, []);
      this.filters = uniqueCategories;
    },
    updateSelectedFilter(newFilter) {
      this.selectedFilter = newFilter;
      this.filterItems();
    },
    updateSortOrder(newSortOrder) {
      const [sortCriteria, sortOrder] = newSortOrder.split("-");
      this.sortOrder = sortOrder;
      this.sortCriteria = sortCriteria;
      this.page = 1;
      this.items = [];
      this.loadData();
    },
    filterItems() {
      if (this.selectedFilter === "all") {
        this.filteredItems = this.items;
      } else {
        this.filteredItems = this.items.filter((card) => {
          return card.categories.some(
            (category) => category.name === this.selectedFilter
          );
        });
      }
    },
  },
};
</script>

<style>
.wrapper {
  width: 100%;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: center;
  gap: 1rem;
}
</style>
