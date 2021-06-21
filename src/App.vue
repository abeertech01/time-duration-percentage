<template>
  <div class="app">
    <div class="content">
      <img src="./assets/time.svg" />
      <p>You can get percentage number of a time duration from a total time</p>
      <div class="the-time time-input">
        <h2>The Time</h2>
        <input type="number" placeholder="hh" v-model="theHour" />
        <span> : </span>
        <input type="number" placeholder="mm" v-model="theMin" />
      </div>

      <div class="total-time time-input">
        <h2>Total Time</h2>
        <input type="number" placeholder="hh" v-model="totalHour" />
        <span> : </span>
        <input type="number" placeholder="mm" v-model="totalMin" />
      </div>
      <button class="result-btn" @click="getResult">Get Result</button>

      <div class="result">Result: {{ result }}%</div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  name: "App",
  setup() {
    const result = ref(0);

    // The Time
    const theHour = ref(null);
    const theMin = ref(null);

    // The Time
    const totalHour = ref(null);
    const totalMin = ref(null);

    const totalTheMin = ref(null);
    const totalTotalMin = ref(null);

    const getResult = function () {
      if (theHour.value && theMin.value && totalHour.value && totalMin.value) {
        totalTheMin.value = Number(theHour.value * 60) + Number(theMin.value);
        totalTotalMin.value =
          Number(totalHour.value * 60) + Number(totalMin.value);

        result.value = (
          (totalTheMin.value * 100) /
          totalTotalMin.value
        ).toFixed(2);

        if (result.value % 1 === 0) {
          result.value = Math.ceil(result.value);
        }
      }
    };

    return {
      result,
      theHour,
      theMin,
      totalHour,
      totalMin,
      getResult,
    };
  },
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Philosopher:wght@400;700&display=swap");

* {
  padding: 0;
  margin: 0;
}
html,
body {
  box-sizing: border-box;
  font-family: "Philosopher", sans-serif;
}
.app {
  width: 100vw;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;

  .content {
    width: 300px;
    text-align: center;

    img {
      width: 100%;
    }

    p {
      font-size: 19px;
      margin-bottom: 15px;
    }

    .time-input {
      input {
        width: 60px;
        outline: none;
        padding: 5px;
        font-size: 18px;
      }

      span {
        font-weight: bolder;
      }
    }

    .the-time {
      margin-bottom: 50px;
    }

    .result-btn {
      margin-top: 10px;
      padding: 5px 10px;
      font-size: 16px;
      background-color: rgb(139, 52, 253);
      border: none;
      font-weight: 600;
      color: white;
      border-radius: 5px;
      cursor: pointer;
    }

    .result {
      margin-top: 40px;
      font-size: 20px;
    }
  }
}
</style>
