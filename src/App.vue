<template>
  <div>
    <Calculator />
  </div>
</template>

<script>
import Calculator from "./components/calculator";
export default {
  components: {
    Calculator,
  },
};
</script>

<style>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
.flex {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background-color: rgb(63, 63, 63);
}

.calculator {
  width: 90%;
  max-width: 430px;
  padding: 25px;
  border-radius: 25px;
  background: linear-gradient(to bottom right, #524f4f, #0c0c0c);
}

/* input */
.input-wrap {
  position: relative;
  width: calc(100% - 4px);
  margin-bottom: 5px;
  padding: 0 5px;
  background: #a1bd66;
  text-align: right;
  box-shadow: inset 0px 0px 15px 0px rgba(0, 0, 0, 0.5);
}

.input {
  height: 5rem;
  line-height: 5rem;
  font-size: 2rem;
}

.smalltext {
  position: absolute;
  right: 5px;
  top: 0.25rem;
  color: grey;
}

/* button */
.button-wrap {
  display: flex;
  width: 100%;
  flex-wrap: wrap;
  justify-content: space-around;
}

.button-wrap > button {
  width: calc(25% - 4px);
  text-align: center;
  line-height: 5rem;
  margin: 2px 0;
  background: grey;
  color: #f1f1f1;
  border-radius: 4px;
  cursor: pointer;
  user-select: none;
  outline: 0;
  transition: 0.3s;
}

.button-wrap > button.largeno {
  width: 75%;
}
.button-wrap > button.clear {
  width: 50%;
}

.button-wrap > button.number {
  background: #5d5d5f;
}

.button-wrap > button:hover {
  box-shadow: inset 0px 0px 15px 0px rgba(0, 0, 0, 0.3);
}

.button-wrap > button.result {
  background: #f55530;
}
</style>
