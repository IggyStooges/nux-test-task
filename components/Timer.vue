<template>

  <div class="timer">
    <div class="timer__time">
      {{ min }}
      <span> м </span>
    </div>
    <span>&nbsp; : &nbsp;</span>
    <div class="timer__time">
      {{ sec }}
      <span> с </span>
    </div>
  </div>

</template>


<script>
  export default {
    data: function () {
      return {
        sec: 0,
        min: 0,
        now: Date.now()
      };
    },
    methods: {
      upSec() {
        this.sec = Math.floor(((Date.now() - this.now) / 1000) % 60);
        this.min = Math.floor(((Date.now() - this.now) / 1000) / 60);
      },
    },

    created() {
      setInterval(() => {
        this.upSec();
      }, 1000);

    }
  }

</script>

<style>
  .timer {
    width: 35%;
    box-sizing: border-box;
    padding: 2%;
    display: flex;
    align-items: flex-end;
    align-self: center;
    justify-content: center;
    margin-left: auto;
    font-weight: 800;
    font-size: 15px;
    color: #35495e;
    border: 3px solid #35495e;
    border-radius: 5px;
  }

  .timer span {
    font-size: 10px;
  }

</style>
