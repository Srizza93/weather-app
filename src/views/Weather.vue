<template>
  <div class="weather">
    <card class="card-wrapper" :info="weather.location" />
    <img
      class="weather-icon"
      v-if="weather.current"
      :src="weather.current.condition.icon"
      alt="weather-icon"
    />
    <card class="card-wrapper" :info="weather.current" />
  </div>
</template>

<script>
import Card from "../components/Card.vue";

export default {
  name: "Weather",
  components: { Card },
  data() {
    return {
      weather: {},
      city: "Lille",
    };
  },
  methods: {
    async fetchData() {
      try {
        const url = `https://api.weatherapi.com/v1/current.json?key=9090010261984f75bd8163005222011&q=${this.city}&aqi=no`;
        const response = await fetch(url)
          .then((response) => {
            if (response.ok) {
              return response.json();
            } else if (response.status === 400) {
              this.redirectToNotFound();
              return Promise.reject("Selected city is incorrect");
            } else {
              this.redirectToNotFound();
              return Promise.reject("Something went wrong: " + response.status);
            }
          })
          .then((data) => (this.weather = data));
      } catch (error) {
        console.log("Can't get data from API: " + error);
      }
    },
    redirectToNotFound() {
      this.$router.push("/NotFound");
    },
  },
  mounted() {
    this.city = this.$route.params.city;
    this.fetchData();
  },
};
</script>

<style lang="scss" scoped>
.weather {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.card-wrapper {
  padding: $standard-distance;
  margin: $standard-distance;
  border: 1px solid rgba(235, 235, 235, 0.64);
}

.weather-icon {
  width: 100px;
}
</style>
