<template>
  <div>
    <div class="block">
      <div class="container">
        {{ text }}
      </div>

      <div class="wrapper">
        <input v-model="inputText" class="input-text" />
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

    const send = () => {
      text.value = inputText.value;
      inputText.value = " ";
    };

    return {
      text,
      inputText,
      send
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
  font-weight:bold;
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