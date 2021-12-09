<template>
  <div id="tech-type">
    <b-container>
      <h1>YOUR TECHNE</h1>
      <b-row>
        <b-col>
          <b-button
            variant="outline-primary"
            @click="chooseTechType(techTypes[0])"
            >{{ techTypes[0].text }}</b-button
          >
        </b-col>
        <b-col>
          <b-button
            variant="outline-primary"
            @click="chooseTechType(techTypes[1])"
            >{{ techTypes[1].text }}</b-button
          >
        </b-col>
      </b-row>
      <b-row>
        {{ techType.explanation }}
      </b-row>
      <b-row>
        <b-col>
          <b-btn
            v-if="techType.id"
            variant="outline-primary"
            @click="clearTechType()"
          >
            Clear
          </b-btn>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>
<script>
import { mapState } from "vuex";

export default {
  data() {
    return {
      techTypes: [
        {
          id: 1,
          text: "Tech Enabled",
          explanation:
            "Tech-enabled companies aren’t building the internet, mobile devices or social media platforms; they’re using those technologies.",
        },
        {
          id: 2,
          text: "Tech Intensive",
          explanation:
            "Tech Intensive companies build the hardware, software, algorithms and platforms.",
        },
      ],
    };
  },
  methods: {
    chooseTechType(item) {
      this.$store.commit("updateTechType", item);
    },
    clearTechType() {
      this.$store.commit("unSetTechType");
      console.log("clearTechType");
    },
  },
  computed: {
    ...mapState(["techType"]),
  },
};
</script>
