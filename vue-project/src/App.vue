<template>
  <div class="block">
    <button @click="switchTheme" :class="['input-button', { '-dark': isDark }]">
      Включить {{ !isDark ? "темную" : "светлую" }} тему
    </button>

    <FormWrapper :isDark="isDark" />

    <div class="burger-item" v-for="burger of burgersStub" :key="burger">
      <img :src="burger.image" class="image" alt="" />
      <div>
        <b>{{ burger.title }}</b>
        <p class="text-description">{{ burger.description }}</p>
      </div>
      <div class="order-button">
        <button class="ord-button">Купить</button>
        <button class="ord-button gray">Подробнее</button>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, onMounted } from "vue";
import FormWrapper from "@/components/FormWrapper.vue";
import { burgersStub } from "@/components/stubs/burgers";

export default {
  components: {
    FormWrapper,
  },
  setup() {
    const isDark = ref(false);

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
      if (localStorage.isDarkTheme === "true") {
        isDark.value = true;
        setDarkTheme(false);
      }
    });

    return {
      switchTheme,
      burgersStub,
      isDark,
    };
  },
};
</script>

<style>
.block {
  width: 50%;
  margin: 0 auto;
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
  grid-template-columns: 144px 2fr 150px;
  align-items: center;
  gap: 16px;
  margin-bottom: 35px;
  padding: 16px;
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
  box-shadow: 0px 5px 16px 2px rgba(34, 60, 80, 0.2);
}
</style> 