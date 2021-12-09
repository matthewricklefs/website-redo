<template>
  <div id="funding">
    <b-container>
      <h1>HOW ARE YOU FUNDED</h1>
      <b-row>
        <b-col>
          <b-button
            variant="outline-primary"
            @click="selectFundingType(fundTypes[0])"
          >
            {{ fundTypes[0].text }}
          </b-button>
        </b-col>
        <b-col>
          <b-button
            variant="outline-primary"
            @click="selectFundingType(fundTypes[1])"
          >
            {{ fundTypes[1].text }}
          </b-button>
        </b-col>
        <b-col>
          <b-button
            variant="outline-primary"
            @click="selectFundingType(fundTypes[2])"
          >
            {{ fundTypes[2].text }}
          </b-button>
        </b-col>
      </b-row>
      <b-row>
        <b-col>
          <b-button
            variant="outline-primary"
            @click="selectFundingType(fundTypes[3])"
          >
            {{ fundTypes[3].text }}
          </b-button>
        </b-col>
        <b-col>
          <b-button
            variant="outline-primary"
            @click="selectFundingType(fundTypes[4])"
          >
            {{ fundTypes[4].text }}
          </b-button>
        </b-col>
        <b-col>
          <b-button
            variant="outline-primary"
            @click="selectFundingType(fundTypes[5])"
          >
            {{ fundTypes[5].text }}
          </b-button>
        </b-col>
      </b-row>
      <b-row>
        {{ fundingType.explanation }}
      </b-row>
      <b-row>
        <b-col>
          <b-button
            v-if="fundingType.id"
            variant="outline-primary"
            @click="unSelectFundingType()"
          >
            clear
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
      fundTypes: [
        {
          id: 1,
          text: "Unfunded",
          explanation:
            "You are not funded. You are looking for ways to raise capital",
          image: null,
        },
        {
          id: 2,
          text: "FFF",
          explanation:
            "The Friends, Family and Foolish have blessed you with limited capital",
          image: null,
        },
        {
          id: 3,
          text: "Bootstraped",
          explanation:
            "You have funded this from a previous succesfull venture or you are independently wealthy",
          image: null,
        },
        {
          id: 4,
          text: "Seeded",
          explanation:
            "You went through an accelerator or have won multiple pitch competitions, maybe both!",
          image: null,
        },
        {
          id: 5,
          text: "Series A",
          explanation:
            "You have raised capital through a formal raise. Investors think you have a great idea but you need to figure out how to monetize it",
          image: null,
        },
        {
          id: 6,
          text: "Series B",
          explanation:
            "You have a great track record and have the funds and confidence of many investors. Now you are looking to break into cutting edge tech and enhance your current offerings. There are more series beyond B in store for you",
          image: null,
        },
      ],
    };
  },
  computed: {
    ...mapState(["fundingType"]),
  },
  methods: {
    selectFundingType(arg) {
      this.$store.commit("updateFundingType", arg);
    },
    unSelectFundingType() {
      this.$store.commit("unSetFundingType");
    },
  },
};
</script>
