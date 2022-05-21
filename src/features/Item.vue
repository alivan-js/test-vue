<template>
  <div class="item" @mouseover.prevent.stop="onHover(true)" @mouseleave="onHover(false)" :class="{ delete: deleted }">
    <img v-if="item.imgUrl" class="item__img" :src="item.imgUrl" alt="Item">
    <img v-else class="item__img" src="../assets/item.png" alt="Item">
    <div class="item__body">
      <span class="item__title">{{ item.title }}</span>
      <span class="item__description">{{ item.description ? item.description : "Описание отсутствует" }}</span>
      <span class="item__price">{{ item.price.toLocaleString('ru') }} руб.</span>
    </div>
    <div class="delete-btn" v-if="hover" @click="deleteItem(item.id)">
      <img src="../assets/delete.svg" alt="DeleteIcon">
    </div>
  </div>
</template>

<script>

export default {
  name: 'app-Item',
  components: {},
  props: {
    item: {
      type: Object,
      required: true
    },
  },
  data() {
    return {
      hover: false,
      deleted: false
    }
  },

  methods: {
    onHover(value) {
      this.hover = value
    },
    deleteItem(id) {
      this.deleted = true
      setTimeout(() => {
        this.$emit("delete", id)
      }, 1000)
    },

  }
}

</script>

<style scoped lang="scss">

.item {
  display: flex;
  flex-direction: column;
  width: 332px;
  position: relative;
  background: #FFFEFB;
  box-shadow: 0 20px 30px rgba(0, 0, 0, 0.04), 0 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 4px;
  overflow-wrap: break-word;
  opacity: 1;
  transition: opacity 1s, height 0s;

  &:hover {
    cursor: pointer;
  }

  &__img{
    width: 332px;
    height: 200px;
  }

  &__body{
    padding: 16px;
    display: flex;
    flex-direction: column;
  }

  &__title {
    font-weight: 600;
    font-size: 20px;
    line-height: 25px;
    color: #3F3F3F;
  }

  &__description {
    font-weight: 400;
    font-size: 16px;
    line-height: 20px;
    color: #3F3F3F;
    margin-bottom: 32px;
  }

  &__price {
    font-weight: 600;
    font-size: 24px;
    line-height: 30px;
    color: #3F3F3F;
    margin-bottom: 8px;
  }

}

.delete-btn {
  width: 32px;
  height: 32px;
  position: absolute;
  top: -8px;
  right: -8px;
  display: flex;
  justify-content: center;
  align-items: center;
  background: #FF8484;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  border-radius: 10px;
}

.delete {
  opacity: 0;
  transition: opacity 1s, height 1s;
  height: 0;
}

@media (max-width: 480px) {

  .item {
    margin: 0 auto;
  }

}

</style>
