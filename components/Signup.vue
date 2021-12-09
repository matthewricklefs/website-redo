<template>
  <div class="signup-app">
    <b-container>
      <div
        v-bind:class="{
          'scale-in-top': signUp.show,
          'scale-out-top': !signUp.show,
        }"
      >
        <b-form @submit="onSubmit" @reset="onReset">
          <b-form-group label="Email">
            <b-form-input
              v-model="signUp.email"
              type="email"
              placeholder="Enter email"
              required
            ></b-form-input>
          </b-form-group>
          <b-form-group label="Name">
            <b-form-input
              v-model="signUp.name"
              placeholder="Enter name"
              required
            ></b-form-input>
          </b-form-group>
          <b-form-group label="Description">
            <b-form-textarea
              v-model="signUp.description"
              placeholder="Describe your idea"
              required
            ></b-form-textarea>
          </b-form-group>
          <b-button type="submit" variant="outline-success"
            >Signup Now</b-button
          >
        </b-form>
      </div>
      <div
        v-bind:class="{
          'scale-in-top': !signUp.show,
          'signup-initial': signUp.show,
          'signup-final': !signUp.show,
        }"
        class="text-pop-up-bottom"
      >
        <b-row>
          <b-col>
            <span>
              <h1>Thanks for signing up!</h1>
            </span>
          </b-col>
        </b-row>
      </div>
    </b-container>
  </div>
</template>

<script>
import { mapState, mapGetters } from "vuex";
export default {
  computed: {
    ...mapState(["signUp"]),
    ...mapGetters(["checksPassed"]),
  },
  data() {
    return {};
  },
  methods: {
    async onSubmit(e) {
      e.preventDefault();
      const payload = {
        email: this.signUp.email,
        description: this.signUp.description,
        name: this.signUp.name,
      };
      // check signup
      this.$store.dispatch("checkOnboarding");
      // submit singup only if checks pass
      if (this.checksPassed) {
        const s = await this.$store.commit("updateSignUp", payload);
        const res = await this.$store.dispatch("onboard");
      } else {
        console.log("missing startup details!");
      }
    },
    onReset(e) {
      e.preventDefault();
      // this.form.name = '';
      // this.form.description = '';
      // this.form.email = '';
      // this.show = false;
      // this.$nextTick(() => {
      //   this.show = true;
      // })
    },
  },
};
</script>
