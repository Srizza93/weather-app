<template>
  <div>
    Weather Component
    <span>{{ weather }}</span>
  </div>
</template>

<script>
export default {
  name: "Weather",
  data() {
    return {
      weather: {},
      city: "Lille",
    };
  },
  methods: {
    async fetchData() {
      try {
        const url = `http://api.weatherapi.com/v1/current.json?key=9090010261984f75bd8163005222011&q=${this.city}&aqi=no`;
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

<style></style>
