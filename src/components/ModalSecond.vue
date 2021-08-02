<template>
  <Modal title="second modal" @close="$emit('close')">
    <div slot="body">
      <form @submit.prevent="submitSecondForm">
        <label for="name">Name</label>
        <input type="text" id="name" v-model="modalSecond.name" required />
        <label for="email">email</label>
        <input type="email" id="email" v-model="modalSecond.email" required />
        <button class="btn btnPrimary">Submit</button>
      </form>
    </div>
  </Modal>
</template>

<script>
import Modal from "@/components/UI/Modal.vue";

export default {
  components: { Modal },

  data() {
    return {
      modalSecond: {
        name: "",
        email: "",
      },
    };
  },

  methods: {
    submitSecondForm() {
      console.log({
        name: this.modalSecond.name,
        email: this.modalSecond.email,
      });
      (this.modalSecond.name = ""), (this.modalSecond.email = "");
      this.$emit("close");
    },
  },
};
</script>