<template>
  <div class="select">
    <div class="option"
         @click="setClick"
    >
      {{ initValue }}
      <img src="../../assets/arrow-down.svg"
           class="option-arrow" alt="arrow">
    </div>
    <div class="options"
         v-if="open">
      <div class="option"
           @click="changeOption(option.name)"
           :key="i" v-for="(option, i) of options"
      >
        {{ option.value }}
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'app-select',
  data() {
    return {
      open: false,
    }
  },
  props: {
    modelValue: {
      type: String
    },
    initValue: {
      type: String
    },
    options: {
      type: Array,
    },
  },
  methods: {
    setClick() {
      this.open = !this.open;
    },
    changeOption(value) {
      this.open = false
      this.$emit("changeOption", value)
    }
  }
}

</script>

<style lang="scss" scoped>

.select {
  cursor: pointer;
  position: relative;
  display: flex;
  flex-direction: column;
  background-color: #FFFEFB;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
  z-index: 1000;
  width: 140px;
}

.options {
  position: absolute;
  top: 30px;
  left: 0;
  background-color: #FFFEFB;
  border-radius: 4px 4px 4px 4px;
}

.option {
  width: 140px;
  height: 36px;
  display: flex;
  justify-content: center;
  align-items: center;
  font-weight: 400;
  font-size: 12px;
  line-height: 15px;
  color: #B4B4B4;
  border-radius: 4px;
}

.option-arrow {
  display: block;
  margin-left: 5px;
}

</style>
