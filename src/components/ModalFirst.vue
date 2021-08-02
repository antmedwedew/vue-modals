<template>
  <Modal title="first modal" @close="$emit('close')">
    <div slot="body">
      <p>text text text text</p>
      <button class="btn btnPrimary">button</button>
    </div>
  </Modal>
</template>

<script>
import Modal from "@/components/UI/Modal.vue";

export default {
  components: { Modal },
};
</script>