<template>
  <section class="center-center">
    <nuxt-content class="markdown" :document="page" />
  </section>
</template>

<script>
export default {
  async asyncData({ $content }) {
    return {
      page: await $content('home').fetch(),
    }
  },
}
</script>

<style lang="sass" scoped>
h2
  margin: 0 0 .25rem 0
</style>
