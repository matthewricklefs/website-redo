<template>
  <div class="onboarding">
    <NavBar
      class="is-sticky"
      v-bind:style="{ top: topPosition + 'px' }"
    ></NavBar>
    <div class="container tab-wrapper">
      <b-tabs align="center">
        <b-tab>
          <template #title>
            <BIconCompass />
            Stage
            <b-badge
              pill
              variant="danger"
              v-if="checks.startupCycle === false"
              class="flicker-1"
              >!</b-badge
            >
          </template>
          <StartupCycle></StartupCycle>
        </b-tab>
        <b-tab>
          <template #title>
            <BIconRecordCircleFill />
            Priority
            <b-badge
              pill
              variant="danger"
              v-if="checks.projectPriorities === false"
              class="flicker-1"
              >!</b-badge
            >
          </template>
          <ProjectPriority></ProjectPriority>
        </b-tab>
        <b-tab>
          <template #title>
            <BIconGearWideConnected />
            Tech Type
            <b-badge
              pill
              variant="danger"
              v-if="checks.techType === false"
              class="flicker-1"
              >!</b-badge
            >
          </template>
          <TechType />
        </b-tab>
        <b-tab title-link-class="industry-tab">
          <template #title>
            <BIconBuilding />
            Industry
            <b-badge
              pill
              variant="danger"
              v-if="checks.industrySelection === false"
              class="flicker-1"
              >!</b-badge
            >
          </template>
          <industry-selection></industry-selection>
        </b-tab>
        <b-tab title-link-class="business-tab">
          <template #title>
            <BIconBoundingBox />
            Business Model
            <b-badge
              pill
              variant="danger"
              v-if="checks.businessModel === false"
              class="flicker-1"
              >!</b-badge
            >
          </template>
          <BusinessModel />
        </b-tab>
        <b-tab title-link-class="funding-tab">
          <template #title>
            <BIconCashStack />
            Funding
            <b-badge
              pill
              variant="danger"
              v-if="checks.fundingType === false"
              class="flicker-1"
              >!</b-badge
            >
          </template>
          <Funding />
        </b-tab>
        <b-tab title-link-class="description-tab">
          <template #title>
            <BIconFileEarmarkText />
            Description
            <!-- <b-badge 
              pill 
              variant="danger" 
              v-if="checks.startupCycle === false"
              class="flicker-1"
            >!</b-badge> -->
          </template>
          <Signup />
        </b-tab>
      </b-tabs>
    </div>
    <Footer />
  </div>
</template>
<script>
import NavBar from "../components/NavBar.vue";
import StartupCycle from "../components/StartupCycle";
import ProjectPriority from "../components/ProjectPriority";
import TechType from "../components/TechType.vue";
import IndustrySelection from "../components/IndustrySelection.vue";
import BusinessModel from "../components/BusinessModel.vue";
import Funding from "../components/Funding.vue";
import Signup from "../components/Signup.vue";

import Footer from "../components/Footer.vue";

import {
  BIconCompass,
  BIconRecordCircleFill,
  BIconGearWideConnected,
  BIconBuilding,
  BIconBoundingBox,
  BIconCashStack,
  BIconFileEarmarkText,
} from "bootstrap-vue";

import { mapState } from "vuex";

export default {
  components: {
    NavBar,
    StartupCycle,
    ProjectPriority,
    TechType,
    IndustrySelection,
    BusinessModel,
    Funding,
    BIconCompass,
    BIconRecordCircleFill,
    BIconGearWideConnected,
    BIconBuilding,
    BIconBoundingBox,
    BIconCashStack,
    BIconFileEarmarkText,
    Signup,
    Footer,
  },
  data() {
    return {
      topPosition: 0,
    };
  },
  computed: {
    ...mapState(["checks"]),
  },
  methods: {
    handleScroll() {
      this.topPosition = window.scrollY;
    },
  },
  mounted() {
    window.addEventListener("scroll", this.handleScroll);
  },
  beforeDestroy() {
    window.removeEventListener("scroll", this.handleScroll);
  },
};
</script>
