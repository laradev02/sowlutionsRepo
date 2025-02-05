<template>
  <div class="container">
    <h2>Search</h2>
    <input
      type="text"
      v-model="searchQuery"
      placeholder="Search..."
      class="search-box"
    />
    <p>{{ filteredArticles.length }} posts were found.</p>

    <div v-for="article in filteredArticles" :key="article.id" class="article">
      <h3 v-html="highlightText(article.title)"></h3>
      <p>
        <em>{{ article.date }}</em>
      </p>
      <p v-html="highlightText(article.content)"></p>
    </div>
  </div>
</template>

<script>
import { articles } from "../assets/data.js";
export default {
  data() {
    return {
      searchQuery: "",
      articles,
    };
  },
  computed: {
    filteredArticles() {
      if (!this.searchQuery) return this.articles;
      return this.articles.filter((article) =>
        (article.title + article.content)
          .toLowerCase()
          .includes(this.searchQuery.toLowerCase())
      );
    },
  },
  methods: {
    highlightText(text) {
      if (!this.searchQuery) return text;
      const regex = new RegExp(`(${this.searchQuery})`, "gi");
      return text.replace(regex, '<span class="highlight">$1</span>');
    },
  },
};
</script>

<style scoped src="../assets/styles.css"></style>
