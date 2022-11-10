<template>
  <div class="block">
    <button @click="switchTheme" :class="['input-button', { '-dark': isDark }]">
      Включить {{ !isDark ? "темную" : "светлую" }} тему
    </button>

    <div class="container">
      {{ text }}
    </div>
    <div class="wrapper">
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
    <div class="order-button">
      <button class="ord-button">Купить</button>
      <button class="ord-button gray">Подробнее</button>
    </div>
    <div class="burger-item" v-for="burger of burgers" :key="burger">
      <img :src="burger.image" class="image" alt="" />
      <div>
        <b>{{ burger.title }}</b>
        <p class="text-description">{{ burger.description }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, onMounted } from "vue";

export default {
  setup() {
    const text = ref("Поле для ввода текста ниже");
    const inputText = ref(null);
    const hasError = ref(false);
    const errorText = ref("");
    const isDark = ref(false);

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

    const switchTheme = () => {
      isDark.value = !isDark.value;
      localStorage.isDarkTheme = isDark.value;
      setDarkTheme(document.querySelector("#dark-theme-style") || false);
    };

    const setDarkTheme = (darkTheme) => {
      if (!darkTheme) {
        const darkThemeLinkEl = document.createElement("link");
        darkThemeLinkEl.setAttribute("rel", "stylesheet");
        darkThemeLinkEl.setAttribute("href", "/src/dark-mode.css");
        darkThemeLinkEl.setAttribute("id", "dark-theme-style");

        document.querySelector("head").append(darkThemeLinkEl);
      } else {
        darkTheme.parentNode.removeChild(darkTheme);
      }
    };

    onMounted(() => {
      if ( localStorage.isDarkTheme === 'true') {
        isDark.value = true
        setDarkTheme(false);
      }
    });

    return {
      text,
      inputText,
      send,
      setErrorVisability,
      switchTheme,
      errorText,
      hasError,
      burgers,
      isDark,
    };
  },
};
</script>

<style>
/* body {
  padding: 0;
  margin: 0;
  height: 100vh;
}

#app {
  background: rgba(116, 193, 245, 0.274);
  height: 100%;
  width: 100%;
} */

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
  width: 94%;
  margin-top: 10px;
  background: rgb(224, 74, 74);
  border-radius: 6px;
  color: rgb(255, 255, 255);
  text-decoration: none;
  padding: 8px 15px;
}
.image {
  width: 150px;
  box-shadow: 9px 1px 17px 4px rgba(55, 57, 59, 0.16);
  margin-bottom: 1px;
}
.burger-item {
  background: #f4f4f4;
  border: 15px;
  border-radius: 6px;
  display: grid;
  grid-template-columns: 144px 2fr;
  align-items: center;
  gap: 16px;
}
.text-description {
  margin-bottom: 0;
  padding: 20px;
  border-radius: 10px;
  color: rgb(0, 0, 0);
  text-align: center;
  font-weight: none;
  box-shadow: 0px 5px 16px 2px rgba(34, 60, 80, 0.2);
}
.order-button {
  display: grid;
  row-gap: 5px;
}
.ord-button {
  width: 30%;
  margin-bottom: 0px;
  font-size: 14px;
  cursor: pointer;
  border-radius: 7px;
  border: none;
  padding: 8px 15px;
  text-decoration: none;
  background: #f88221;
  box-shadow: 0px 5px 16px 2px rgba(34, 60, 80, 0.2);
}

.ord-button.gray {
  background: #b4b2b2;
  margin-bottom: 40px;
  box-shadow: 0px 5px 16px 2px rgba(34, 60, 80, 0.2);
}
</style> 