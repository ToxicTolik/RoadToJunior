<template>
  <div class="main-container">
    <div v-for="(burger, index) of burgers" :key="index" class="burger-wrapper">
      <img class="image" :src="burger.image" />
      <div>
        <b>{{ burger.title }}</b>
        <p>{{ burger.description }}</p>
      </div>
      <div class="button-content">
        <button class="base-button">Купить</button>
        <button class="base-button gray">Подробнее</button>
      </div>
    </div>

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
.main-container {
  width: 70%;
  margin: 0 auto;
  font-family: 'Roboto', sans-serif;
  padding-top: 20px;
}
.container {
  /* background: #f4f4f4; */
  margin-top: 99px;
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

/* Стили для бургеров */
.burger-wrapper {
  display: grid;
  gap: 16px;
  grid-template-columns: 144px 2fr 140px;
  align-items: center;
  margin-bottom: 20px;
  box-shadow: -4px 4px 20px 4px rgba(194, 194, 194, 0.25);
  border-radius: 10px;
  padding: 13px
}
.button-content {
  display: grid;
  row-gap: 16px;
}
.base-button {
  width: 100%;
  font-size: 14px;
  cursor: pointer;
  background: #EE7203;
  border-radius: 7px;
  border: none;
  text-decoration: none;
  color: white;
  padding: 10px 20px;
}
.base-button.gray {
  background: #D0D0D0;
}
.image {
  width: 144px;
}
p {
  margin-bottom: 0;
}
</style>