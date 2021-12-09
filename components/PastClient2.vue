<template>
  <div class="past-client" v-bind:style="{ backgroundColor: background }">
    <div>
      <b-row v-if="position === 'left'">
        <b-col>
          <a :href="weblink">
            <img class="client-logo" :src="logo" />
          </a>
        </b-col>
        <b-col>
          <div class="client-about">
            <div>
              {{ quote }}
              <br />
              <br />
              {{ impact }}
            </div>
          </div>
        </b-col>
      </b-row>
      <b-row v-else-if="position === 'right'">
        <b-col>
          <div class="client-about">
            <div>
              {{ quote }}
              <br />
              <br />
              {{ impact }}
            </div>
          </div>
        </b-col>
        <b-col>
          <a :href="weblink">
            <img class="client-logo" :src="logo" />
          </a>
        </b-col>
      </b-row>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    name: {
      type: String,
      required: true,
    },
    logo: String,
    quote: String,
    background: String,
    position: String,
    weblink: String,
    impact: String,
  },
  data() {
    return {};
  },
  computed: {},
  methods: {},
};
</script>
