<template>
  <div class="card" style="width: 400px">
    <img
      class="card-img-top"
      :src="image"
      alt="Card image"
      style="width: 100%"
    />
    <div class="card-body">
      <p class="card-title bold h3"><strong v-html="name"></strong></p>
      <p class="card-subtitle h6">{{ this.formatCategories }}</p>
      <div v-html="description" class="card-text"></div>
      <AddToCard />
    </div>
  </div>
</template>

<script>
import AddToCard from "./AddToCard.vue";

export default {
  name: "CardItem",
  props: ["image", "name", "category", "description"],
  computed: {
    formatCategories() {
      if (this.category) {
        return this.category.map((cat) => cat.name).join(", ");
      }
      return "";
    },
  },
  components: { AddToCard },
};
</script>

<style>
img {
  object-fit: contain;
}
.card {
  border: 1px solid #dddddd;
  padding: 10px;
  border-radius: 10px;
  min-width: 300px;
}
.card-subtitle {
  color: gray;
  font-weight: bold;
}
</style>
