<template>
  <Header />

  <div class="layout">
    <div class="layout__content">

      <section class="about">
        <h2>About</h2>
        <p>
          An Vue Template to build WebApps for DZD
        </p>

        <h2>How-to</h2>
        <p>
          Enter a gene name (e.g. FOXA2) to perform demo request, which shows all PubMed results for this Gene in Humans.
        </p>
      </section>

      <slot />
    </div>
  </div>
  <Footer />
</template>
<script>
  import Footer from './Footer.vue';
  import Header from './Header.vue';
  export default {
    name: 'Layout',
    components: {
      Footer, Header,
    }
  }
</script>
<style lang="scss">
  .layout {
    padding-top: 0 !important;
  }
</style>