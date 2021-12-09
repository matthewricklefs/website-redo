<template>
  <b-navbar id="navbar" toggleable type="dark">
    <b-navbar-brand href="">
      <router-link to="/">
        <!-- CYBER CONCEPTS -->
        <b-img :src="logo"></b-img>
      </router-link>
    </b-navbar-brand>
    <b-nav-text> CYBER CONCEPTS </b-nav-text>
    <b-navbar-toggle target="navbar-toggle-collapse">
      <template #default="{ expanded }">
        <b-icon v-if="expanded" icon="x-circle"></b-icon>
        <b-icon v-else icon="list"></b-icon>
      </template>
    </b-navbar-toggle>

    <b-collapse id="navbar-toggle-collapse" is-nav>
      <b-navbar-nav class="ml-auto">
        <b-nav-item>
          <router-link to="/">Home</router-link>
        </b-nav-item>
        <!-- <b-nav-item>
            <router-link to="/services">Services</router-link>
          </b-nav-item> -->
      </b-navbar-nav>
    </b-collapse>
  </b-navbar>
</template>

<script>
import logo from "../assets/cc_logo_1_sm_wht.svg";

export default {
  data() {
    return {
      logo: logo,
    };
  },
};
</script>
