<template>
  <section id="breach-list">
    <div v-if="loading" class="loading">
      LOADING RECENT BREACHES...
    </div>
    <div v-if="breaches.length">
      <Breach :id="breach.Name" :breach="breach" v-for="breach in breaches.slice(0, maxBreaches)" :key="breach.Name" />
    </div>
  </section>
</template>

<script>
import axios from "axios";
import Breach from "./Breach.vue";

function dateSort(key) {
  return (itemA, itemB) => new Date(itemB[key]) - new Date(itemA[key]);
}

export default {
  name: "BreachList",
  components: {
    Breach
  },
  data() {
    return {
      breaches: [],
      sensitiveBreaches: [],
      loading: true
    };
  },
  methods: {
    async getBreaches(breachURL) {
      const res = await axios.get(breachURL);
      this.breaches = res.data
        .filter(
          breach =>
            breach.IsVerified && !breach.IsFabricated && !breach.IsRetired
        )
        .sort(dateSort("AddedDate"));

      this.sensitiveBreaches = this.breaches.filter(
        breach => breach.IsSensitive
      );

      this.loading = false;
    }
  },
  props: {
    maxBreaches: Number
  },
  mounted() {
    setInterval(() => {
      this.getBreaches("https://haveibeenpwned.com/api/v2/breaches");
    }, 100);
  }
};
</script>

<style lang="scss" scoped>
.loading {
  color: green;
}
</style>
