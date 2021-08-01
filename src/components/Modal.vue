<template>
  <transition name="modal">
    <div class="modal" @click="$emit('close')">
      <div class="modal__content" @click.stop="">
        <!-- header -->
        <div class="modal__header">
          <div class="modal__title">{{ title }}</div>
          <span class="modal__close" @click="$emit('close')">×</span>
        </div>

        <!-- body -->
        <div class="modal__body">
          <slot name="body">default body</slot>
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
      required: true,
    },
  },
  mounted() {
    document.body.addEventListener("keyup", (e) => {
      if (e.keyCode === 27) {
        this.$emit("close");
      }
    });
  },
};
</script>

<style lang="scss" scoped>
// animation
.modal-enter,
.modal-leave-active {
  opacity: 0;
}

.modal-enter .modal__content,
.modal-leave-active .modal__content {
  transform: scale(1.2);
}

.modal {
  display: flex;
  justify-content: center;
  align-items: center;
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  transition: opacity 0.2s ease;
  right: 0;
  z-index: 998;
  background-color: rgba(00, 00, 00, 0.48);

  &__content {
    position: relative;
    max-width: 600px;
    padding: 20px 18px;
    background-color: #fff;
    border: 1px solid #dcdfe6;
    transition: all 0.2s ease;
    border-radius: 8px;
    z-index: 999;
    overflow: hidden;
    @media screen and (min-width: 900px) {
      min-width: 500px;
    }
  }

  &__title {
    font-size: 24px;
  }

  &__header {
    display: flex;
    align-self: center;
    justify-content: space-between;
    padding-bottom: 20px;
  }

  &__body {
    text-align: center;
  }

  &__close {
    cursor: pointer;
    font-size: 45px;
    line-height: 36px;
  }
}
</style>
