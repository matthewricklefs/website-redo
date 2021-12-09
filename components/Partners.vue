<template>
  <div>
    <b-container class="partners-container">
      <h1>Sister Organizations and Companies</h1>
      <b-row v-for="(item, key) in sisterOrgs" :key="key">
        <b-card no-body>
          <b-row no-gutters>
            <b-col md="3" :class="item.img_container_class">
              <b-card-img :src="item.logo" :class="item.img_class"></b-card-img>
            </b-col>
            <b-col md="9">
              <b-card-body :title="item.title">
                <b-card-text>
                  {{ item.content }}
                  <br />
                  <br />
                  <br />
                  <b-link :href="item.webLink">
                    <b-btn variant="outline-primary">Checkout</b-btn>
                  </b-link>
                </b-card-text>
              </b-card-body>
            </b-col>
          </b-row>
        </b-card>
      </b-row>
    </b-container>
  </div>
</template>
<script>
export default {
  components: {},
  props: {
    sisterOrgs: Array,
  },
  data() {
    return {};
  },
};
</script>
