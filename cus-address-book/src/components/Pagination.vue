<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <div class="pagination">
    <div class="page-info">
      Showing data {{ startDataIndex }} to {{ endDataIndex }} of {{ totalEntries }} entries
    </div>
    <div class="page-numbers">
      <button @click="goToPage(1)" :disabled="currentPage === 1">&lt;</button>
      <span v-for="page in displayedPages" :key="page">
        <button @click="goToPage(page)" :class="{ 'active': page === currentPage }">{{ page }}</button>
      </span>
      <button @click="goToPage(totalPages)" :disabled="currentPage === totalPages">&gt;</button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    currentPage: Number,
    totalPages: Number,
    totalEntries: Number,
    itemsPerPage: Number,
  },
  computed: {
    startDataIndex() {
      const startIndex = (this.currentPage - 1) * this.itemsPerPage + 1;
      return isNaN(startIndex) ? 0 : startIndex;
    },
    endDataIndex() {
      const endIndex = this.currentPage * this.itemsPerPage;
      const validEndIndex = Math.min(endIndex, this.totalEntries);
      return isNaN(validEndIndex) ? 0 : validEndIndex;
    },
    //calculates an array of page numbers to be displayed in the pagination component
    displayedPages() {
      const totalDisplayedPages = 3;
      const pages = [];
      const halfDisplay = Math.floor(totalDisplayedPages / 2);

      //Ensure displayed page numbers are within the valid range of available pages
      for (let i = Math.max(1, this.currentPage - halfDisplay); i <= Math.min(this.totalPages, this.currentPage + halfDisplay); i++) {
        pages.push(i);
      }

      return pages;
    },
  },
  methods: {
    goToPage(page) {
      this.$emit('page-change', page);
    },
  },
};
</script>

<style scoped>
.pagination {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-top: 20px;
}

.page-info {
  font-size: 14px;
}

.page-numbers {
  display: flex;
  align-items: center;
}

.page-numbers button {
  margin: 0 5px;
  padding: 5px 10px;
  cursor: pointer;
  border: 1px solid #ccc;
  border-radius: 5px;
  background-color: #fff;
}

.page-numbers button.active {
  background-color: purple;
  color: #fff;
}

.page-numbers button:disabled {
  cursor: not-allowed;
}
</style>
