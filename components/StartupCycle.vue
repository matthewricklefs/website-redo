<template>
  <div id="startup-cycle-app">
    <b-row class="startup-cycle-title">
      <b-col md="3"></b-col>
      <b-col md="6"><h1>WHERE ARE YOU?</h1></b-col>
      <b-col md="3"></b-col>
    </b-row>
    <!-- Where are you in the startup cycle? -->
    <!-- An interactive set of circles with lines attatching them on a path -->
    <k v-for="(item, key) in stages" :key="key">
      <div
        :class="item.class"
        @click="
          choosesStartupCycle({
            id: item.id,
            text: item.text,
            explanation: item.explanation,
          })
        "
      >
        <p>{{ item.text }}</p>
      </div>
    </k>
    <div>
      <b-row class="startup-cycle-explanation">
        {{ startupCycle.explanation }}
      </b-row>
      <br />
      <br />
      <b-row class="ctl-row">
        <b-col>
          <b-btn
            v-if="startupCycle.id"
            variant="outline-primary"
            @click="clearStartupCycle()"
          >
            Clear
          </b-btn>
        </b-col>
        <!-- <b-col>
          <b-btn v-if="startupCycle.text" variant="outline-primary">{{startupCycle.text}}</b-btn>
        </b-col>
        <b-col>
          <b-btn 
            v-if="startupCycle.id" 
            variant="outline-primary"
            @click="nextTab()"
          >
            Next
          </b-btn>
        </b-col> -->
      </b-row>
    </div>
  </div>
</template>
<script>
import { mapState } from "vuex";

export default {
  data() {
    return {
      stages: [
        {
          id: 1,
          text: "Ideation",
          class: "cycle-node node-1",
          explanation:
            "You are exploring ideas, experimenting with solutions, analyzing industries and markets ripe for disruption. You have yet to choose a single idea but you have the dream.",
        },
        {
          id: 2,
          text: "Proof of Concept",
          class: "cycle-node node-2",
          explanation:
            "You have found how to level the competition to thier knees before you. Now you need to prove your plan is actually possible to implement.",
        },
        {
          id: 3,
          text: "Founders Fit",
          class: "cycle-node node-3",
          explanation:
            "You have found fellow compatriots, henchmen, and malcontents. The dream is becoming real, a goal to be reached and attained.",
        },
        {
          id: 4,
          text: "MVP",
          class: "cycle-node node-4",
          explanation:
            "You have your plan and now you have your core team. Now you need to build your minimum viable product!.",
        },
        {
          id: 5,
          text: "Market Fit",
          class: "cycle-node node-5",
          explanation:
            "You have lanuched! Now you need to get customers, make improvments and get some revenue. Are you missing out on the revenue part? Are you pivoting?",
        },
        {
          id: 6,
          text: "Scale Up",
          class: "cycle-node node-6",
          explanation:
            "You have found your market fit and a growing cusotmer base, congratulations! Can you maintain the growth? Are you adding new features and able to keep your services running smoothly?",
        },
      ],
    };
  },
  computed: {
    ...mapState(["startupCycle"]),
  },
  methods: {
    choosesStartupCycle(args) {
      this.$store.commit("updateStartupCycle", args);
    },
    clearStartupCycle() {
      this.$store.commit("unSetStartupCycle");
    },
  },
};
</script>
