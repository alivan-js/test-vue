<template>
  <button :disabled="disabled" :class="{ disabled: disabled === true }">{{ text }}</button>
</template>

<script>

export default  {
  name: 'app-button',
  components: {},
  props: {
    text: String,
    disabled: Boolean
  },
}

</script>

<style scoped>

button {
  height: 36px;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 10px;
  font-family: 'Inter', sans-serif;
  font-weight: 600;
  font-size: 12px;
  line-height: 15px;
  text-align: center;
  letter-spacing: -0.02em;
  background: #7BAE73;
  color: #FFFFFF;
}

.disabled {
  color: #B4B4B4;
  background: #EEEEEE;
}

</style>
