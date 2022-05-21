<template>
  <div class="side-block">
    <div class="side-block-container">
      <form>
        <Textarea
            label="Наименование товара"
            :isRequired="true"
            :value="title"
            :error="errors.find((el) => el.field === 'title')?.value"
            name="title"
            placeholder="Введите наименование товара"
            @changeInput="changeInputValue"

        />
        <Textarea
            label="Описание товара"
            :isRequired="false"
            :value="description"
            :error="errors.find((el) => el.field === 'description')?.value"
            name="description"
            placeholder="Введите описание товара"
            height="108px"
            @changeInput="changeInputValue"
        />
        <Textarea
            label="Ссылка на изображение товара"
            :isRequired="true"
            :value="imgUrl"
            :error="errors.find((el) => el.field === 'imgUrl')?.value"
            name="imgUrl"
            placeholder="Введите ссылку"
            @changeInput="changeInputValue"
        />
        <Textarea
            label="Цена товара"
            :value="price"
            :error="errors.find((el) => el.field === 'price')?.value"
            :isRequired="true"
            name="price"
            placeholder="Введите цену"
            @changeInput="changeInputValue"

        />
        <Button v-if="errors.length"
                :disabled="true"
                type="submit"
                value="Добавить товар"
                @click="addItem"
        />
        <Button v-else
                :disabled="!!errors.length"
                value="Добавить товар"
                @click="addItem"
        />
      </form>
    </div>
  </div>
</template>

<script>

import Button from "@/shared/components/Button";
import Textarea from "@/shared/components/Textarea";

export default {
  name: 'app-addItem',
  components: {
    Textarea, Button
  },
  data() {
    return {
      errors: [""],
      title: "",
      description: "",
      imgUrl: "",
      price: "",
    }
  },
  methods: {
    addItem(e) {

      e.preventDefault()
      this.checkForm()

      if (!this.errors.length) {

        this.$emit("addItem", {
          title: this.title,
          description: this.description,
          imgUrl: this.imgUrl,
          price: +this.price
        })

        this.resetForm()
        this.errors = [""]

      }

    },
    changeInputValue(value) {
      this[value.name] = value.value
      this.checkForm()
    },
    checkForm: function () {

      this.errors = [];

      let urlRegex = /^(https?|chrome):\/\/[^\s$.?#].[^\s]*$/

      if (!this.title) {
        this.errors.push({field: "title", value: 'Требуется указать название товара'});
      }
      if (!this.imgUrl) {
        this.errors.push({field: "imgUrl", value: 'Требуется указать ссылку на товар'});
      }
      if (!urlRegex.test(this.imgUrl)) {
        this.errors.push({field: "imgUrl", value: 'Неверный формат данных'});
      }
      if (!this.price) {
        this.errors.push({field: "price", value: 'Требуется указать цену товара'});
      }
      if (!isFinite(+this.price)) {
        this.errors.unshift({field: "price", value: 'Неверный формат данных'});
      }

    },
    resetForm() {
      this.title = ""
      this.description = ""
      this.imgUrl = ""
      this.price = ""
    }
  }
}
</script>

<style scoped lang="scss">

.side-block {
  margin-right: 16px;
}

.side-block-container {
  position: sticky;
  top: 25px;
  width: 332px;
  padding: 24px;
  background-color: #FFFEFB;
  box-shadow: 0 20px 30px rgba(0, 0, 0, 0.04), 0 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 4px;
  font-weight: 400;
  font-size: 10px;
  line-height: 13px;
  letter-spacing: -0.02em;
  color: #49485E;

  div {
    margin-bottom: 16px;
  }

}

@media (max-width: 480px) {

  .side-block {
    margin-bottom: 8px;
    margin-right: 0;
  }
}

</style>
