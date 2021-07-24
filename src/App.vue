<template>
  <div class="wrapper">
    <div class="wrapper-content">
      <div class="container">
        <!-- first modal -->
        <button class="btn btnPrimary" @click="modalFirst = !modalFirst">
          modal first
        </button>
        <Modal
          v-if="modalFirst"
          title="first modal"
          @close="modalFirst = !modalFirst"
        >
          <div slot="body">
            <p>text text text text</p>
            <button class="btn btnPrimary">button</button>
          </div>
        </Modal>
      </div>
    </div>
  </div>
</template>

<script>
import Modal from "@/components/Modal.vue";

export default {
  components: { Modal },

  data() {
    return {
      modalFirst: false,
    };
  },
};
</script>