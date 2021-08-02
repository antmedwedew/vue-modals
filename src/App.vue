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
      </div>
    </div>
  </div>
</template>

<script>
import ModalFirst from "@/components/ModalFirst.vue";
import ModalSecond from "@/components/ModalSecond.vue";

export default {
  components: { ModalFirst, ModalSecond },

  data() {
    return {
      modalFirst: false,
      modalSecond: false,
    };
  },
};
</script>