<template>
  <nav aria-label="Page navigation example">
    <ul class="pagination">
      <!-- 前一頁 previousPage -->
      <li v-show="prev" :class="['page-item', { disabled: currentPage === 1 }]">
        <router-link
          :to="{
            name: 'restaurants',
            query: { categoryId, page: prev },
          }"
          class="page-link"
          aria-label="Previous"
        >
          <span aria-hidden="true">&laquo;</span>
        </router-link>
      </li>

      <li
        v-for="page in totalPage"
        :key="page"
        :class="['page-item', { active: page === currentPage }]"
      >
        <router-link
          class="page-link"
          :to="{ name: 'restaurants', query: { categoryId, page } }"
        >
          {{ page }}
        </router-link>
      </li>

      <!-- 後一頁 nextPage -->
      <li
        v-show="next"
        :class="['page-item', { disabled: currentPage === totalPage.length }]"
      >
        <router-link
          class="page-link"
          aria-label="Next"
          :to="{ name: 'restaurants', query: { categoryId, page: next } }"
        >
          <span aria-hidden="true">&raquo;</span>
        </router-link>
      </li>
    </ul>
  </nav>
</template>

<script>
export default {
  props: {
    categoryId: {
      type: [String, Number],
      default: "",
    },
    currentPage: {
      type: Number,
      default: 1,
    },
    totalPage: {
      type: Array,
      required: true,
    },
    next: {
      type: Number,
      required: true,
    },
    prev: {
      type: Number,
      required: true,
    },
  },
};
</script>