<template>
  <div class="pitch-div" v-bind:style="pitch.styleObject">
    <div
      v-if="pitch.assets.backgroundImage"
      class="wrapper"
      v-bind:style="{
        backgroundImage: `url('${pitch.assets.backgroundImage}')`,
        backgroundSize: 'cover',
        backgroundPosition: 'center',
      }"
    >
      <div v-if="pitch.assets.centerImage">
        <img
          class="center-image"
          :src="require(`../assets/${pitch.assets.centerImage}`)"
        />
      </div>
      <div class="center">
        {{ pitch.champion }}
      </div>
    </div>
    <div class="wrapper" v-else>
      <div v-if="pitch.assets.centerImage">
        <img
          class="center-image"
          :src="require(`../assets/${pitch.assets.centerImage}`)"
        />
      </div>
      <div class="center">
        {{ pitch.champion }}
      </div>
    </div>
    <br />
  </div>
</template>
<script>
export default {
  props: {
    pitch: Object,
  },
  data() {
    return {};
  },
};
</script>
