<template>
  <div>
    <nav>
      <ul class="pagination">
        <li
          v-for="page in pages"
          :data-test="`page-link-${page}`"
          :key="page"
          :class="paginationClass(page)"
          @click.prevent="changePage(page);"
        >
          <a href="" class="page-link" v-text="page"></a>
        </li>
      </ul>
    </nav>
  </div>
</template>

<script>
export default {
  name: "Vpagination",
  props: {
    pages: {
      type: Array,
      required: true
    },
    currentPage: {
      type: Number,
      required: true
    }
  },
  methods: {
    changePage(gotToPage) {
      if (gotToPage === this.currentPage) return;
      this.$emit("update:currentPage", gotToPage);
    },
    paginationClass(page) {
      return {
        "page-item": true,
        active: this.currentPage === page
      };
    }
  }
};
</script>

<style lang="scss" scoped>
</style>
