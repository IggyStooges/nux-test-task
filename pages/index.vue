<template>
  <section class="container">
    <app />
  </section>
</template>

<script>
  import App from '~/components/App.vue'
  import Field from "~/components/Field.vue";
  import Timer from "~/components/Timer.vue";

  export default {
    components: {
      App,
      Field,
      Timer
    }
  }

</script>

<style>
  .container {
    margin: 5% auto;
  }

</style>
