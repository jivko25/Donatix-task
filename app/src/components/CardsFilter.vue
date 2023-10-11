<template>
    <div class="wrapper">
      <select class="form-select" v-model="selectedFilter" @change="filterChanged">
        <option value="all">Всички</option>
        <option v-for="filter in filters" :value="filter.name" :key="filter.id">
          {{ filter.name }}
        </option>
      </select>
      <select class="form-select" v-model="sortOrder" @change="sortChanged">
        <option value="default">Сортиране по</option>
        <option value="&orderby=title-&order=asc">Име &#11165;</option>
        <option value="&orderby=title-&order=desc">Име &#11167;</option>
        <option value="&orderby=price-&order=asc">Цена &#11165;</option>
        <option value="&orderby=price-&order=desc">Цена &#11167;</option>
      </select>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      filters: Array,
    },
    data() {
      return {
        selectedFilter: "all",
        sortOrder: "default",
      };
    },
    methods: {
      filterChanged() {
        this.$emit("filter-selected", this.selectedFilter);
      },
      sortChanged() {
        this.$emit("sort-order-changed", this.sortOrder);
      },
    },
  };
  </script>
  
  <style scoped>
  .wrapper {
    margin-bottom: 1rem;
    display: flex;
    justify-content: center;
  }
  
  select {
    max-width: 300px;
  }
  </style>
  