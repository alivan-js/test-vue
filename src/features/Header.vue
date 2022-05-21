<template>
  <header class="header">
    <div class="side-block-title">Добавление товара</div>
    <AddItem v-if="isMobile"
             @addItem="addNewItem"
    />
    <Select :options="options"
            :initValue="optionInitValue"
            @changeOption="changeOption"></Select>
  </header>
</template>

<script>

import AddItem from "@/features/AddItem";
import Select from "@/shared/components/Select";

export default {
  name: 'app-header',
  components: {Select, AddItem},
  props: {
    isMobile: Boolean,
  },
  data() {
    return {
      options: [
        {name: "ascendingPrice", value: "По возрастанию цены"},
        {name: "descendingPrice", value: "По убыванию цены"},
        {name: "descendingTitle", value: "По наименованию"},
      ],
      optionInitValue: "По умолчанию"
    }
  },
  methods: {
    changeOption(name) {
      this.optionInitValue = this.options.find(el => el.name === name).value
      this.$emit("sortItems", name)
    },
    addNewItem(value) {
      this.$emit("addItem", value)
    },
  }
}

</script>

<style lang="scss" scoped>

.header {
  display: flex;
  justify-content: space-between;
  padding-bottom: 16px;
}

.side-block-title {
  display: inline-block;
  font-size: 28px;
  line-height: 35px;
}

@media (max-width: 480px) {

  .header {
    padding-bottom: 8px;
    flex-direction: column;
    align-items: center;
  }

  .items {
    gap: 8px;
  }

  .side-block-title {
    margin-bottom: 4px;
  }

}

</style>
