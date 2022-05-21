<template>
  <div>
    <label :class="{required: isRequired === true}" for="name">{{ label }}</label>
    <textarea :class="{errorTextarea: !!error === true}"
              id="name"
              :name="name"
              :value="value"
              @input="event => changeInput({value:  event.target.value.trim(), name})"
              rows="0"
              :placeholder="placeholder"
              :style="{height: `${height}`}"
    />
    <p v-if="error" class="errorMessage">{{ error }}</p>
  </div>
</template>

<script>

export default {
  name: 'app-textarea',
  components: {},
  props: {
    label: String,
    placeholder: String,
    height: String,
    value: String,
    name: String,
    isRequired: Boolean,
    error: String
  },
  methods: {
    changeInput(value) {
      this.$emit("changeInput", value)
    }
  }
}

</script>

<style lang="scss" scoped>

label {
  display: inline-block;
  margin-bottom: 4px;
  position: relative;
}

.required {
  &:after {
    content: " ";
    display: block;
    height: 4px;
    width: 4px;
    position: absolute;
    top: 0;
    right: -4px;
    border-radius: 50%;
    background: #FF8484;
  }
}

textarea {
  width: 100%;
  height: 36px;
  padding: 10px 16px;
  overflow: hidden;
  background: #FFFEFB;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
  font-weight: 400;
  font-size: 12px;
  line-height: 15px;
  color: #3F3F3F;
  resize: none;

  &::placeholder {
    font-weight: 400;
    font-size: 12px;
    line-height: 15px;
    color: #B4B4B4;
  }

  &:focus {
    box-shadow: 3px 3px 3px 3px rgba(0, 0, 0, 0.15);
  }

}

.errorMessage {
  font-weight: 400;
  font-size: 8px;
  line-height: 10px;
  margin-top: 4px;
  letter-spacing: -0.02em;
  color: #FF8484;
}

.errorTextarea {
  border: 1px solid #FF8484;
}

</style>
