<template>
  <div class="wrapper">
    <div class="wrapper-content">
      <div class="container">
        <!-- first modal -->
        <button class="btn btnPrimary" @click="modalFirst = !modalFirst">
          modal first
        </button>
        <ModalFirst @close="modalFirst = false" v-show="modalFirst" />

        <!-- second modal -->
        <button class="btn btnPrimary" @click="modalSecond = !modalSecond">
          modal second
        </button>
        <ModalSecond @close="modalSecond = false" v-show="modalSecond" />

        <!-- validate modal -->
        <button class="btn btnPrimary" @click="modalValidate = !modalValidate">
          modal validate
        </button>
        <ModalValidate @close="modalValidate = false" v-show="modalValidate" />
      </div>
    </div>
  </div>
</template>

<script>
import ModalFirst from "@/components/ModalFirst.vue";
import ModalSecond from "@/components/ModalSecond.vue";
import ModalValidate from "@/components/ModalValidate.vue";

export default {
  components: { ModalFirst, ModalSecond, ModalValidate },

  data() {
    return {
      modalFirst: false,
      modalSecond: false,
      modalValidate: false,
    };
  },
};
</script>

<style lang="scss" scoped>
.btn {
  margin-right: 10px;
}
</style>