<template>
  <article :class="{breach, sensitive: breach.IsSensitive, 'no-domain': !breach.Domain}">
    <header>
      <img :src="breach.LogoPath" class="breach-logo" />
      <h2>{{ breach.Title }}</h2>
    </header>
    <dl>
      <dt>Domain:</dt>
      <dd class="domain">{{ breach.Domain }}</dd>

      <dt>Pwn Count:</dt>
      <dd class="pwn-count">{{ breach.PwnCount.toLocaleString() }}</dd>

      <dt>Added Date:</dt>
      <dd class="added-date">{{ new Date(breach.AddedDate).toLocaleDateString() }}</dd>

      <dt>Description:</dt>
      <dd v-html="breach.Description"></dd>

      <dt>Data Classes:</dt>
      <dd>
        <ul>
          <li v-for="dataClass in breach.DataClasses" :key="dataClass">{{dataClass}}</li>
        </ul>
      </dd>
    </dl>
  </article>
</template>

<script>
export default {
  name: "Breach",
  props: {
    breach: Object
  }
};
</script>

<style lang="scss" scoped>
.breach {
  border-top: 1px dashed black;
  margin: 20px 50px;
  padding: 10px;
  text-align: left;

  &.sensitive {
    background-color: rgba(salmon, 0.333);
  }

  &.no-domain {
    background-color: rgba(gold, 0.333);
  }

  .domain:empty::after {
    color: red;
    content: "None";
  }

  .breach-logo {
    float: right;
    max-width: 100px;
  }

  dt {
    font-weight: bolder;
  }

  dd ul {
    margin: 0;
    padding: 0;
  }
}
</style>
