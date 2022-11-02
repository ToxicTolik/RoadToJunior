<template>
  <div>
    <div class="block">
      <div class="container">
        {{ text }}
      </div>

      <div class="wrapper">
        <input v-model="inputText" @input="setErrorVisability" class="input-text" />
        <button @click="send" class="input-button">Отправить</button>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  setup() {
    const text = ref("Тестовый текст");
    const inputText = ref(null);
    const hasError = ref(false);

    const send = () => {
      if (!inputText.value) {
        hasError.value = true
        console.log(hasError.value)
        return
      }

      text.value = inputText.value;
      inputText.value = "";
    };

    const setErrorVisability = () => {
      hasError.value = false
    };

    return {
      text,
      inputText,
      send,
      setErrorVisability,
    };
  },
};
</script>

<style>
.block {
  width: 50%;
}
.container {
  background: rgb(184, 183, 183);
  padding: 50px;
  border-radius: 10px;
  color: rgb(0, 0, 0);
  text-align: center;
  font-weight: bold;
}
.wrapper {
  display: flex;
  justify-content: space-between;
  gap: 10px;
  width: 100%;
  margin-top: 10px;
}
.input-text {
  width: 100%;
}
.input-button {
  width: 30%;
  cursor: pointer;
  color: rgb(0, 0, 0);
  border-radius: 6px;
  border-style: outset;
  background: rgb(224, 74, 74);
}
</style>