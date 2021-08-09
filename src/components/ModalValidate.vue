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

        <!-- email -->
        <div class="form__item" :class="{ error: $v.email.$error }">
          <label for="email">email</label>
          <p class="form__error-text" v-if="!$v.email.required">
            Filled is required!
          </p>
          <p class="form__error-text" v-if="!$v.email.email">
            Email is not correct!
          </p>
          <input
            id="email"
            v-model.trim="email"
            @change="$v.email.$touch()"
            :class="{ error: $v.email.$error }"
          />
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
        </div>

        <!-- repeatPassword -->
        <div class="form__item" :class="{ error: $v.repeatPassword.$error }">
          <label for="repeatPassword">repeatPassword</label>
          <p class="form__error-text" v-if="!$v.repeatPassword.required">
            Filled is required!
          </p>
          <p class="form__error-text" v-if="!$v.repeatPassword.$error">
            Repeat password!
          </p>
          <p class="form__error-text" v-if="!$v.repeatPassword.sameAsPassword">
            Passwords must be identical!
          </p>
          <input
            id="repeatPassword"
            v-model.trim="repeatPassword"
            @change="$v.repeatPassword.$touch()"
          />
        </div>
        <!-- button submit -->
        <button class="btn btnPrimary">Submit</button>
      </form>
    </div>
  </Modal>
</template>

<script>
import { required, minLength, email, sameAs } from "vuelidate/lib/validators";

import Modal from "@/components/UI/Modal.vue";

export default {
  components: { Modal },

  data() {
    return {
      name: "",
      email: "",
      password: "",
      repeatPassword: "",
    };
  },
  validations: {
    name: {
      required,
      minLength: minLength(2),
    },
    email: {
      required,
      email,
    },
    password: {
      required,
      minLength: minLength(6),
    },
    repeatPassword: {
      required,
      sameAsPassword: sameAs("password"),
    },
  },
  methods: {
    onSubmit() {
      this.$v.$touch();

      if (!this.$v.$invalid) {
        const user = {
          name: this.name,
          email: this.email,
          password: this.password,
          repeatPassword: this.repeatPassword,
        };
        console.log(user);
        this.close();
      }
    },
    close() {
      this.$emit("close");
      this.$v.$reset();
      this.name = "";
      this.email = "";
      this.password = "";
      this.repeatPassword = "";
    },
  },
};
</script>

<style lang="scss">
.form {
  $form: &;

  &__error-text {
    display: none;
    margin-bottom: 10px;
    font-size: 13px;
    color: #ff3c3c;
  }

  &__item {
    &.error {
      #{$form}__error-text {
        display: block;
      }

      input {
        border-color: #ff3c3c;
      }
    }
  }
}
</style>