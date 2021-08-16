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

        <!-- sing in / sing up -->
        <!-- sing in -->
        <button class="btn btnPrimary" @click="ModalSingIn = !ModalSingIn">
          Sing in
        </button>
        <ModalSingIn @close="ModalSingIn = false" v-show="ModalSingIn" />

        <!-- sing up -->
        <button class="btn btnPrimary" @click="ModalRegister = !ModalRegister">
          Register
        </button>
        <ModalRegister @close="ModalRegister = false" v-show="ModalRegister" />
      </div>
    </div>
  </div>
</template>

<script>
import ModalFirst from "@/components/ModalFirst.vue";
import ModalSecond from "@/components/ModalSecond.vue";
import ModalValidate from "@/components/ModalValidate.vue";
import ModalRegister from "@/components/ModalRegister.vue";
import ModalSingIn from "@/components/ModalSingIn.vue";

export default {
  components: {
    ModalFirst,
    ModalSecond,
    ModalValidate,
    ModalRegister,
    ModalSingIn,
  },

  data() {
    return {
      modalFirst: false,
      modalSecond: false,
      modalValidate: false,
      modalSingIn: false,
      ModalRegister: false,
      ModalSingIn: false,
    };
  },
};
</script>

<style lang="scss" scoped>
.btn {
  margin-right: 10px;
}
</style>