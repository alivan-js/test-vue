<template>
  <div class="modal-backdrop">
    <div class="modal">
      <div class="modal__header">
        {{message}}
      </div>
      <div class="modal__body">
        <Button @click="closeItem" :text="buttonValue"/>
      </div>
    </div>
  </div>
</template>

<script>

import Button from "@/shared/components/Button";

export default {
  name: 'app-modal',
  components: {
    Button
  },
  props: {
    message: String,
    buttonValue: String,
  },
  methods: {
    closeItem() {
      this.$emit('close');
    },
  },
};

</script>

<style lang="scss" scoped>

.modal-backdrop {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: rgba(0, 0, 0, 0.3);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1001;
}

.modal {
  height: 150px;
  width: 200px;
  border-radius: 4px;
  background: #FFFFFF;
  box-shadow: 2px 2px 20px 1px;
  overflow-x: auto;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
  padding: 5px;

  &__header {
    font-size: 20px;
    text-align: center;
  }

  &__body {
    width: 100%;
  }

}

</style>
