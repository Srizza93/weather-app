<template>
  <div class="home-container">
    <div class="input-container">
      <input
        class="input-container_input"
        type="text"
        placeholder="Add your city!"
        v-model="city"
        @keyup.enter="citySelected"
      />
      <div class="input-container_button-wrap">
        <router-link
          class="input-container_button-wrap_button"
          :to="{ name: 'weather', params: { city: city } }"
          >Go!</router-link
        >
      </div>
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
.input-container {
  display: flex;
  flex-direction: row;
}
.input-container_input {
  height: 35px;
  padding: 0 10px;
  border-radius: 10px 0 0 10px;
  border: none;
  border-right: solid #181818 1px;
  font-size: 18px;
}
.input-container_input:focus {
  outline: none;
}
.input-container_button-wrap_button {
  padding: 5px;
  font-weight: bold;
  text-decoration: none;
}
.input-container_button-wrap_button:hover {
  opacity: 0.7;
}
</style>

<style lang="scss" scoped>
.input-container_button-wrap {
  display: flex;
  align-items: center;
  border-radius: 0 10px 10px 0;
  background-color: $primary-color;
}
.input-container_button-wrap_button {
  color: $secondary-color;
}
</style>
