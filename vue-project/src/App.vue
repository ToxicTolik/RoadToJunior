<template>
  <div class="block">
    <div class="container">
      {{ text }}
    </div>
    <div class="wrapper">
      <input
        v-model="inputText"
        @input="setErrorVisability"
        class="input-text"
      />
      <button @click="send" class="input-button">Отправить</button>
    </div>
    <div v-show="hasError" class="error-message">
      {{ errorText }}
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
    const errorText = ref("");
    const burgers = [
      {
        title: "Шримп Ролл",
        description:
          "Нежные креветки в хрустящей панировке, свежий салат Айсберг и лук в пшеничной лепешке, заправленной специальным соусом.",
        image:
          "https://ma-prod-cdn.mcdonalds.ru/product/c69d517219a348a283c2d8fd06c77ff1/android/l/main.png",
      },
      {
        title: "Биг Спешиал Три Сыра",
        description:
          "Новое прочтение всем знакомого бургера. Большой сочный бифштекс из 100% говядины, приготовленный на гриле. Три вкуснейших сыра: нежный Эмменталь, сливочный Гауда и плавленый Чеддер в виде топпинга. Свежие овощи и знаменитый соус с дымком",
        image:
          "https://ma-prod-cdn.mcdonalds.ru/product/520e14b577a74b75a5f515dd26daa38d/android/l/main.png",
      },
      {
        title: "Чикен Премьер",
        description:
          "Сочная куриная котлета в хрустящей панировке, сыр Чеддер, ароматный бекон, ломтик помидора, свежий салат, специальный соус и булочка с кунжутом",
        image:
          "https://ma-prod-cdn.mcdonalds.ru/product/95956070e293461eaa9bb2ebcec10895/android/l/main.png",
      },
    ];

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
      send,
      setErrorVisability,
      errorText,
      hasError,
      burgers,
    };
  },
};
</script>

<style>
.block {
  width: 50%;
  margin: 0 auto;
}
.container {
  /* background: #f4f4f4; */
  padding: 50px;
  border-radius: 10px;
  color: rgb(0, 0, 0);
  text-align: center;
  font-weight: bold;
  box-shadow: 0px 5px 16px 2px rgba(34, 60, 80, 0.2);
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
  border: none;
  text-decoration: none;
  color: white;
}
.input-button:hover {
  background: green;
}
.error-message {
  width: 100%;
  margin-top: 10px;
  background: rgb(224, 74, 74);
  border-radius: 6px;
  color: white;
  text-decoration: none;
}
</style>