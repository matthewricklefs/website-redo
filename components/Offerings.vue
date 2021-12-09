<template>
  <div>
    <b-container class="offerings-container">
      <b-row
        class="offerings-row"
        v-for="(item, key) in serviceOfferings"
        :key="key"
      >
        <b-col>
          <b-card
            :title="item.title"
            :img-src="item.image"
            :class="item.class"
            :id="item.id"
            v-on:click="offeringClicked(item.title)"
            v-b-toggle="item.collapseId"
          >
            <b-card-text>
              <b-collapse :id="item.collapseId">
                <p v-for="(text, tkey) in item.content" :key="tkey">
                  {{ text }}
                </p>
              </b-collapse>
            </b-card-text>
          </b-card>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>
<script>
export default {
  props: {
    serviceOfferings: Array,
  },
  data() {
    return {};
  },
  methods: {
    offeringClicked(offerId) {
      this.$emit("offering-clicked", offerId);
    },
  },
};
</script>
