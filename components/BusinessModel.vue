<template>
  <div id="startup-business-model">
    <!-- What is your business model, B2B, B2C or B2G -->
    <b-container>
      <h1>BUSINES MODEL</h1>
      <b-row>
        <b-col>
          <b-button
            variant="outline-primary"
            @click="selectBusinessModel(businessModels[0])"
          >
            {{ businessModels[0].text }}
          </b-button>
        </b-col>
        <b-col>
          <b-button
            variant="outline-primary"
            @click="selectBusinessModel(businessModels[1])"
          >
            {{ businessModels[1].text }}
          </b-button>
        </b-col>
        <b-col>
          <b-button
            variant="outline-primary"
            @click="selectBusinessModel(businessModels[2])"
          >
            {{ businessModels[2].text }}
          </b-button>
        </b-col>
      </b-row>
      <b-row>{{ businessModel.explanation }}</b-row>
      <b-row>
        <b-col>
          <b-button
            v-if="businessModel.id"
            variant="outline-primary"
            @click="clearBusinessModel()"
          >
            Clear
          </b-button>
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
      businessModels: [
        {
          id: 1,
          text: "B2B",
          explanation:
            "Business to Business, your customers are businesses. You rely on providing high value solutions",
          image: null,
        },
        {
          id: 2,
          text: "B2C",
          explanation:
            "Business to Consumer, your customers are individuals. You need mass appeal and good customer relations",
          image: null,
        },
        {
          id: 3,
          text: "B2G",
          explanation:
            "Business to Government, your customers are public sector entities. You rely on meeting RFS or RFP requirments",
          image: null,
        },
      ],
    };
  },
  methods: {
    selectBusinessModel(model) {
      this.$store.commit("updateBusinessModel", model);
    },
    clearBusinessModel() {
      this.$store.commit("unSetBusinessModel");
    },
  },
  computed: {
    ...mapState(["businessModel"]),
  },
};
</script>
