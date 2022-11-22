<template>
  <div class="home-container">
    <div>
      <input
        type="text"
        placeholder="Add your city!"
        v-model="city"
        @keyup.enter="citySelected"
      />
      <router-link :to="{ name: 'weather', params: { city: city } }"
        >Go!</router-link
      >
    </div>
  </div>
</template>

<script>
export default {
  name: "Home",
  data() {
    return {
      city: "",
    };
  },
  methods: {
    citySelected(event) {
      this.$router.push({
        name: "weather",
        params: { city: event.target.value },
      });
    },
  },
};
</script>

<style scoped>
.home-container {
  display: flex;
  justify-content: center;
  margin-top: 30px;
}
</style>
