<template>
  <div id="footer">
    <footer class="footer">
      <b-container>
        <ul>
          <li>Copyleft {{ currentYear }}, Attribution</li>
        </ul>
      </b-container>
    </footer>
  </div>
</template>

<script>
export default {
  computed: {
    currentYear() {
      const today = new Date();
      return today.getFullYear();
    },
  },
  data() {
    return {};
  },
};
</script>
