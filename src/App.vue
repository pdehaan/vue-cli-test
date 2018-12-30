<template>
  <main id="app">
    <header>
      <h1>{{ title }}</h1>
      <img alt="Vue logo" src="./assets/logo.png" />
    </header>

    <BreachList :maxBreaches="maxBreaches" />
  </main>
</template>

<script>
import BreachList from "./components/BreachList.vue";

export default {
  name: "app",
  components: {
    BreachList
  },
  data() {
    return {
      // breaches: [],
      // sensitiveBreaches: [],
      title: "Have I Been Pwned?",
      maxBreaches: 35
    };
  }
  // methods: {
  //   async getBreaches(breachURL) {
  //     const { data } = await axios.get(breachURL);
  //     this.breaches = data
  //       .filter(
  //         breach =>
  //           breach.IsVerified && !breach.IsFabricated && !breach.IsRetired
  //       )
  //       .sort(dateSort("AddedDate"));
  //     this.sensitiveBreaches = data.filter(breach => breach.IsSensitive);
  //   }
  // },
  // mounted() {
  //   this.getBreaches("https://haveibeenpwned.com/api/v2/breaches");
  // }
};
</script>

<style>
#app {
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  color: #2c3e50;
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  margin-top: 60px;
  text-align: center;
}
</style>
