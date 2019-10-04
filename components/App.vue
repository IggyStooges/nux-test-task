<template>

  <div class="app">
    <h1 class="title">
      15
    </h1>
    <div class="steps"> шаги : {{ step }}</div>

    <timer></timer>

    <field class="app__field" :step="step"></field>

  </div>

</template>



<script>
  import Field from "./Field";
  import Timer from "./Timer";

  export default {
    components: {
      field: Field,
      timer: Timer
    },
    data: function () {
      return {
        step: 0
      }
    },

  };

</script>



<style>
  .app {
    width: 30%;
    margin: 0 auto;
    display: flex;
    flex-wrap: wrap;
  }

  .app__field {
    width: 100%;
    margin-top: 2%;
  }

  .title {
    padding: 2% 5%;
    margin: 0;
    font-size: 30px;
    font-weight: 800;
    color: #35495e;
    border: 3px solid #35495e;
    border-radius: 5px;
  }

  .steps {
    width: 30%;
    align-self: center;
    margin-left: auto;
    font-weight: 800;
    padding: 2% 1%;
    font-size: 15px;
    color: #35495e;
    border: 3px solid #35495e;
    border-radius: 5px;
  }

</style>
