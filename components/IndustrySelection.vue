<template>
  <div id="startup-industry-selection">
    <!-- What industry is your idea in energy, materials, industrial, consumer services, consumer goods, health care, financials, IT, telecom, utilities -->
    <b-container>
      <h1>YOUR INDUSTRY SECTOR</h1>
      <b-row v-for="(item, key) in chunk(industrySectors, 3)" :key="key">
        <b-col v-for="(i, k) in item" :key="k">
          <b-button variant="outline-info" @click="industrySelected(i)">
            {{ i.sector }}
          </b-button>
        </b-col>
      </b-row>
      <b-row>
        <b-col>
          <b-button
            v-if="industrySelection.id"
            variant="outline-primary"
            @click="industryCleared()"
            >Clear</b-button
          >
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>
<script>
export default {
  data() {
    return {
      industrySectors: [
        {
          id: 1,
          sector: "Energy",
        },
        {
          id: 2,
          sector: "Materials",
        },
        {
          id: 3,
          sector: "Industrial",
        },
        {
          id: 4,
          sector: "Consumer Services",
        },
        {
          id: 5,
          sector: "Consumer Goods",
        },
        {
          id: 6,
          sector: "Health Care",
        },
        {
          id: 7,
          sector: "Financials",
        },
        {
          id: 8,
          sector: "Information Technology",
        },
        {
          id: 9,
          sector: "Telecom",
        },
        {
          id: 10,
          sector: "Utilities",
        },
      ],
    };
  },
  computed: {
    industrySelection: {
      get() {
        return this.$store.state.industrySelection;
      },
      set(selection) {
        this.$store.commit("setIndustrySelection", selection);
      },
    },
  },
  methods: {
    industrySelected(e) {
      this.industrySelection = e;
    },
    industryCleared() {
      this.$store.commit("unSetIndustrySelection");
    },
    chunk(arr, size) {
      return Array.from({ length: Math.ceil(arr.length / size) }, (v, i) =>
        arr.slice(i * size, i * size + size)
      );
    },
  },
};
</script>
