<template>
  <div class="content">
    <div class="items"
         v-if="items.length"
    >
      <Item v-for="item in items"
            :key="item.id"
            :item="item"
            @delete="deleteItem"
      />
    </div>
    <div v-else class="content-empty">
      Нет товаров
    </div>
  </div>
</template>

<script>

import Item from "@/features/Item";

export default {
  name: 'app-itemList',
  components: {Item},
  props: {
    items: Array,
  },
  methods: {
    deleteItem(value) {
      this.$emit("deleteItem", value)
    }
  }
}

</script>

<style scoped>

.items {
  width: 100%;
  display: flex;
  gap: 16px;
  flex-wrap: wrap;
}

.content-empty {
  font-family: 'Source Sans Pro', sans-serif;
  font-style: normal;
  font-weight: 600;
  font-size: 28px;
  line-height: 35px;
  color: #3F3F3F;
}

@media (max-width: 480px) {

  .items {
    gap: 8px;
  }

}

</style>
