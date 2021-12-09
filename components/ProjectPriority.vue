<template>
  <div class="priorities">
    <div>
      <!-- What are you looking for, good, fast, cheap? -->
      <b-container>
        <h1>SET YOUR PRIORITIES</h1>
        <b-row>
          <b-col class="priority-header">
            <h1>{{ priorities.good.text }}</h1>
          </b-col>
        </b-row>
        <b-row>
          <b-col>
            <RoundSlider
              v-model="priorities.good.value"
              :start-angle="priorities.good.startAngle"
              :end-angle="priorities.good.endAngle"
              :radius="priorities.good.radius"
              :class="priorities.good.class"
              :change="priorityGoodChanged"
              pathColor="#fff"
              rangeColor="#fff046"
            ></RoundSlider>
          </b-col>
        </b-row>
        <b-row>
          <b-col class="priority-explanation">
            <h4
              v-if="(priorities.good.value > 0) & (priorities.good.value <= 33)"
            >
              {{ priorities.good.explanation.low }}
            </h4>
            <h4
              v-if="
                (priorities.good.value > 33) & (priorities.good.value <= 66)
              "
            >
              {{ priorities.good.explanation.mid }}
            </h4>
            <h4
              v-if="
                (priorities.good.value > 66) & (priorities.good.value <= 100)
              "
            >
              {{ priorities.good.explanation.high }}
            </h4>
          </b-col>
        </b-row>
        <b-row>
          <b-col class="priority-header">
            <h1>{{ priorities.fast.text }}</h1>
          </b-col>
        </b-row>
        <b-row>
          <b-col>
            <RoundSlider
              v-model="priorities.fast.value"
              :start-angle="priorities.fast.startAngle"
              :end-angle="priorities.fast.endAngle"
              :radius="priorities.fast.radius"
              :class="priorities.fast.class"
              :change="priorityFastChanged"
              pathColor="#fff"
              rangeColor="#65ff3b"
            ></RoundSlider>
          </b-col>
        </b-row>
        <b-row>
          <b-col class="priority-explanation">
            <h4
              v-if="(priorities.fast.value > 0) & (priorities.fast.value <= 33)"
            >
              {{ priorities.fast.explanation.low }}
            </h4>
            <h4
              v-if="
                (priorities.fast.value > 33) & (priorities.fast.value <= 66)
              "
            >
              {{ priorities.fast.explanation.mid }}
            </h4>
            <h4
              v-if="
                (priorities.fast.value > 66) & (priorities.fast.value <= 100)
              "
            >
              {{ priorities.fast.explanation.high }}
            </h4>
          </b-col>
        </b-row>
        <b-row>
          <b-col class="priority-header">
            <h1>{{ priorities.cheap.text }}</h1>
          </b-col>
        </b-row>
        <b-row>
          <b-col>
            <RoundSlider
              v-model="priorities.cheap.value"
              :start-angle="priorities.cheap.startAngle"
              :end-angle="priorities.cheap.endAngle"
              :radius="priorities.cheap.radius"
              :class="priorities.cheap.class"
              :change="priorityCheapChanged"
              pathColor="#fff"
              rangeColor="#4681ff"
            ></RoundSlider>
          </b-col>
        </b-row>
        <b-row>
          <b-col class="priority-explanation">
            <h4
              v-if="
                (priorities.cheap.value > 0) & (priorities.cheap.value <= 33)
              "
            >
              {{ priorities.cheap.explanation.low }}
            </h4>
            <h4
              v-else-if="
                (priorities.cheap.value > 33) & (priorities.cheap.value <= 66)
              "
            >
              {{ priorities.cheap.explanation.mid }}
            </h4>
            <h4
              v-else-if="
                (priorities.cheap.value > 66) & (priorities.cheap.value <= 100)
              "
            >
              {{ priorities.cheap.explanation.high }}
            </h4>
          </b-col>
        </b-row>
        <br />
        <br />
        <b-row>
          <b-col class="priority-header">
            <h2 v-if="priorities.good.value > 0">
              Quality - {{ priorities.good.value }}
            </h2>
            <h2 v-if="priorities.fast.value > 0">
              Speed - {{ priorities.fast.value }}
            </h2>
            <h2 v-if="priorities.cheap.value > 0">
              On Budget - {{ priorities.cheap.value }}
            </h2>
          </b-col>
        </b-row>
        <b-row>
          <b-col>
            <b-btn
              v-if="calculatedPriority > 0"
              variant="outline-primary"
              @click="clearPriorities"
              >Clear</b-btn
            >
          </b-col>
          <!-- <b-col></b-col>
          <b-col>
            <b-btn v-if="calculatedPriority > 0" variant="outline-primary">Next</b-btn>
          </b-col> -->
        </b-row>
      </b-container>
    </div>
  </div>
</template>
<script>
import RoundSlider from "vue-round-slider";

export default {
  components: {
    RoundSlider,
  },
  computed: {
    goodPriority: {
      get() {
        return this.$store.state.projectPriorities.good;
      },
      set: function (payload) {
        this.$store.commit("setProjectPriorities", {
          id: payload.id,
          value: payload.value,
        });
      },
    },
    fastPriority: {
      get() {
        return this.$store.state.projectPriorities.fast;
      },
      set: function (payload) {
        this.$store.commit("setProjectPriorities", {
          id: payload.id,
          value: payload.value,
        });
      },
    },
    cheapPriority: {
      get() {
        return this.$store.state.projectPriorities.cheap;
      },
      set: function (payload) {
        this.$store.commit("setProjectPriorities", {
          id: payload.id,
          value: payload.value,
        });
      },
    },
  },
  data() {
    return {
      priorities: {
        good: {
          id: 1,
          class: "priority-good",
          text: "Quality",
          value: null,
          startAngle: -60,
          endAngle: 240,
          radius: 110,
          explanation: {
            low: "Limited functionality, bad for product launches, good for prototyping ideas",
            mid: "Nominal functionality, useful for steady development of common features",
            high: "Desirable for product launches, cyber security, or research into new tech like Blockchains and AI",
          },
        },
        fast: {
          id: 2,
          class: "priority-fast",
          text: "Speed",
          value: null,
          startAngle: -60,
          endAngle: 240,
          radius: 110,
          explanation: {
            low: "Not happening soon, very bad for scheduling, good for tutoring",
            mid: "Good for steady and reliable scheduling, developing features at a normal pace",
            high: "Rapid turn around times, good for demonstrations to Investors or Venture Capitalists and conference presentations",
          },
        },
        cheap: {
          id: 3,
          class: "priority-cheap",
          text: "Cheap",
          value: null,
          startAngle: -60,
          endAngle: 240,
          radius: 110,
          explanation: {
            low: "It's not gonna be cheap, you should have a large budget",
            mid: "Moderatley expensive, good for managing costs and avoiding cost overages",
            high: "Good for prototyping and proving a concept",
          },
        },
      },
      priorityMax: 150,
      calculatedPriority: 0,
    };
  },
  methods: {
    /**
     * Convenience function.
     */
    updatePriorities() {
      this.goodPriority = {
        id: 1,
        value: this.priorities.good.value,
      };
      this.fastPriority = {
        id: 2,
        value: this.priorities.fast.value,
      };
      this.cheapPriority = {
        id: 3,
        value: this.priorities.cheap.value,
      };
    },
    priorityGoodChanged() {
      this.calculatedPriority =
        this.priorities.good.value +
        this.priorities.cheap.value +
        this.priorities.fast.value;
      if (this.calculatedPriority > this.priorityMax) {
        let diff = this.calculatedPriority - this.priorityMax;
        this.priorities.fast.value = this.priorities.fast.value - diff;
        if (this.priorities.fast.value < 0) {
          let subZero = this.priorities.fast.value;
          this.priorities.cheap.value = this.priorities.cheap.value + subZero;
          this.priorities.fast.value = 0;
        }
      }
      this.updatePriorities();
    },
    priorityFastChanged() {
      this.calculatedPriority =
        this.priorities.good.value +
        this.priorities.cheap.value +
        this.priorities.fast.value;
      if (this.calculatedPriority > this.priorityMax) {
        let diff = this.calculatedPriority - this.priorityMax;
        this.priorities.cheap.value = this.priorities.cheap.value - diff;
        if (this.priorities.cheap.value < 0) {
          let subZero = this.priorities.cheap.value;
          this.priorities.good.value = this.priorities.good.value + subZero;
          this.priorities.cheap.value = 0;
        }
      }
      this.updatePriorities();
    },
    priorityCheapChanged() {
      this.calculatedPriority =
        this.priorities.good.value +
        this.priorities.cheap.value +
        this.priorities.fast.value;
      if (this.calculatedPriority > this.priorityMax) {
        let diff = this.calculatedPriority - this.priorityMax;
        this.priorities.good.value = this.priorities.good.value - diff;
        if (this.priorities.good.value < 0) {
          let subZero = this.priorities.good.value;
          this.priorities.fast.value = this.priorities.fast.value + subZero;
          this.priorities.good.value = 0;
        }
      }
      this.updatePriorities();
    },
    clearPriorities() {
      this.priorities.good.value = null;
      this.priorities.fast.value = null;
      this.priorities.cheap.value = null;
      this.$store.commit("unSetProjectPriorities");
    },
  },
};
</script>
