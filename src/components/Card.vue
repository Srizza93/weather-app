<template>
  <div>
    <ul class="card">
      <li
        v-for="(value, propName, index) of info"
        :key="index + '-infoObject-' + propName"
      >
        <div v-if="propName !== 'icon'">
          <span> {{ capitalizeFirstLetter(propName) }}: </span>
          <span class="card_value" v-if="!isAnObject(value)">
            {{ value }}
          </span>
          <card v-else :info="value" />
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "Card",
  props: {
    info: {
      type: Object,
    },
  },
  methods: {
    isAnObject(value) {
      return typeof value === "object";
    },
    capitalizeFirstLetter(word) {
      return word[0].toUpperCase() + this.replaceUnderscore(word).substring(1);
    },
    replaceUnderscore(propName) {
      if (propName.includes("_")) {
        return propName.replaceAll("_", " ");
      }
      return propName;
    },
  },
};
</script>

<style scoped>
.card {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(160px, 1fr));
  list-style-type: none;
  overflow: hidden;
  padding: 0;
}
.card_value {
  color: white;
  font-weight: bold;
}
</style>
