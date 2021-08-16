<template>
  <Modal title="validate modal" @close="close">
    <div slot="body">
      <form class="form" @submit.prevent="onSubmit">
        <!-- name -->
        <div class="form__item" :class="{ error: $v.name.$error }">
          <label for="name">Name</label>
          <p class="form__error-text" v-if="!$v.name.required">
            Filled is required!
          </p>
          <p class="form__error-text" v-if="!$v.name.minLength">
            Name must have at least {{ $v.name.$params.minLength.min }}!
          </p>
          <input id="name" v-model.trim="name" @change="$v.name.$touch()" />
        </div>

        <!-- password -->
        <div class="form__item" :class="{ error: $v.password.$error }">
          <label for="password">Password</label>
          <p class="form__error-text" v-if="!$v.password.required">
            Filled is required!
          </p>
          <p class="form__error-text" v-if="!$v.password.minLength">
            Password must have at least {{ $v.password.$params.minLength.min }}!
          </p>
          <input
            id="password"
            v-model.trim="password"
            @change="$v.password.$touch()"
          />
          <p v-if="this.textErrorEntry" class="form__error-entry">
            you entered incorrect login details
          </p>
        </div>

        <!-- button submit -->
        <button class="btn btnPrimary">Submit</button>

        <p v-if="this.textSingIn" class="form__success-text">
          you have successfully signed in to your account
        </p>
      </form>
    </div>
  </Modal>
</template>

<script>
import Modal from "@/components/UI/Modal.vue";

import { required, minLength } from "vuelidate/lib/validators";

export default {
  components: { Modal },

  data() {
    return {
      name: "",
      password: "",
      textSingIn: false,
      textErrorEntry: false,
    };
  },

  validations: {
    name: {
      required,
      minLength: minLength(2),
    },
    password: {
      required,
      minLength: minLength(6),
    },
  },

  methods: {
    entryUser() {
      const userData = JSON.parse(localStorage.getItem("userData"));
      const { name, password } = userData;

      if (this.name === name && this.password === password) {
        this.textSingIn = true;
        this.textErrorEntry = false;
        setTimeout(() => {
          this.close();
        }, 2000);
      } else {
        this.textErrorEntry = true;
      }
    },

    onSubmit() {
      this.$v.$touch();

      if (!this.$v.$invalid) {
        this.entryUser();
      }
    },
    close() {
      this.$emit("close");
      this.$v.$reset();
      this.name = "";
      this.password = "";
      this.textSingIn = false;
      this.textErrorEntry = false;
    },
  },
};
</script>

<style lang="scss" scoped>
.form {
  &__success-text {
    color: green;
  }

  &__error-entry {
    color: red;
  }
}
</style>