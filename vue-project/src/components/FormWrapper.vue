<template>
  <div class="main-container">
    <div class="container">
      {{ text }}
    </div>
    <div class="form">
      <input
        v-model="inputText"
        @input="setErrorVisability"
        class="input-text"
      />
      <button @click="send" :class="['input-button', { '-dark': isDark }]">
        Отправить
      </button>
    </div>
    <div v-show="hasError" class="error-message">
      {{ errorText }}
    </div>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  props: {
    isDark: {
      type: Boolean,
      default: false
    }
  },
  setup() {
    const text = ref("Поле для ввода текста ниже");
    const inputText = ref(null);
    const hasError = ref(false);
    const errorText = ref("");

    const send = () => {
      if (!inputText.value || inputText.value.length < 5) {
        hasError.value = true;
        errorText.value = !inputText.value
          ? "Поле не должно быть пустым"
          : "Фраза не должна быть меньше 5 символов";
        return;
      }

      text.value = inputText.value;
      inputText.value = "";
    };

    const setErrorVisability = () => {
      hasError.value = false;
    };

    return {
      text,
      inputText,
      hasError,
      errorText,
      send,
      setErrorVisability
    }
  },
};
</script>

<style scoped>
.main-container {
  margin: 20px 0 50px;
}

.block {
  width: 50%;
  margin: 0 auto;
}
.container {
  background: #f4f4f4;
  padding: 30px;
  border-radius: 10px;
  color: rgb(0, 0, 0);
  text-align: center;
  font-weight: bold;
  box-shadow: 0px 5px 16px 2px rgba(34, 60, 80, 0.2);
}
.form {
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
  border: none;
  text-decoration: none;
  color: white;
  padding: 8px 15px;
}
.input-button:hover {
  background: rgb(255, 145, 1);
  box-shadow: 9px 1px 17px 4px rgba(55, 57, 59, 0.16);
}
.input-button.-dark {
  background: rgb(9, 1, 14);
}

.error-message {
  margin-top: 10px;
  background: rgb(224, 74, 74);
  border-radius: 6px;
  color: rgb(255, 255, 255);
  text-decoration: none;
  padding: 8px 15px;
}
</style> 