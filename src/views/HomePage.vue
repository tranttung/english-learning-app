<template>
  <div>
    <h1>Learn English Vocabulary</h1>
    <button
      v-for="(category, key) in vocabularies"
      :key="key"
      @click="selectCategory(key)"
    >
      {{ key }}
    </button>
    <VocabularyList
      v-if="selectedCategory"
      :title="selectedCategory"
      :words="vocabularies[selectedCategory]"
    />
  </div>
</template>

<script>
import { vocabularies } from "@/data/vocabularies";
import VocabularyList from "@/components/VocabularyList.vue";

export default {
  components: {
    VocabularyList,
  },
  data() {
    return {
      vocabularies,
      selectedCategory: null,
    };
  },
  methods: {
    selectCategory(category) {
      this.selectedCategory = category;
    },
  },
};
</script>

<style scoped>
h1 {
  text-align: center;
  color: #2c3e50;
}
button {
  margin: 5px;
  padding: 10px 15px;
  background-color: #3498db;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}
button:hover {
  background-color: #2980b9;
}
</style>
