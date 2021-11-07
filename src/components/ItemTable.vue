<template>
  <section class="table-item">
    <h2 class="table-item__hl">{{ headline }}</h2>
    <table class="table-item__table">
      <thead>
        <tr>
          <th class="table-item__table-head-name">Name</th>
          <th class="table-item__table-head--isbn">ISBN</th>
          <th class="table-item__table-head--actions"></th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="currentBookList in currentBooksList"
          :key="currentBookList.id"
          class="table-item__table-row"
        >
          <td>{{ currentBookList.title }}</td>
          <td>{{ currentBookList.isbn }}</td>
          <td>
            <button
              :class="{
                'table-item__table-btn-remove': currentBookList.isBookmarked,
                'table-item__table-btn-add': !currentBookList.isBookmarked,
              }"
              @click="bookmarkChanged(currentBookList)"
            >
              <span v-if="currentBookList.isBookmarked"> - entfernen </span>
              <span v-else> + hinzufügen</span>
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </section>
</template>

<script>
export default {
  name: "ItemTable",
  props: {
    headline: {
      type: String,
      required: true,
    },
    currentBooksList: {
      type: Array,
      default: () => [],
    },
  },
  methods: {
    bookmarkChanged(currentBookList) {
      this.$emit("bookmark-changed", currentBookList.id);
    },
  },
};
</script>
