<template>
  <div id="app">
    <div class="head">
      <div>
        <h1>devfinder</h1>
      </div>
      <div
        style="cursor: pointer"
        class="toggle"
        aria-label="Toggle themes"
        @click="toggleTheme"
      >
        <div class="dark-light">
          <span v-if="this.theme == 'darkMode'"> Light</span>
          <span v-else> Dark</span>
        </div>
        <div class="dark-light--icon">
          <img
            v-if="this.theme == 'darkMode'"
            src="./assets/sun-regular.svg"
            alt=""
          />
          <img v-else src="./assets/moon-regular.svg" alt="" />
        </div>
      </div>
    </div>

    <div class="search--input">
      <Search />
    </div>
  </div>
</template>

<script>
import Search from "./components/Search.vue";
export default {
  name: "App",
  components: {
    Search,
  },
  data() {
    return {
      theme: "",
    };
  },
  mounted() {
    document.documentElement.setAttribute("data-theme", this.theme);
  },
  methods: {
    toggleTheme() {
      this.theme = this.theme == "darkMode" ? "" : "darkMode";
      document.documentElement.setAttribute("data-theme", this.theme);
    },
  },
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Rokkitt:wght@300;400&display=swap");

:root {
  --background-color: #e7f2ff;
  --text-color: #1c1c1c;
  --cards-color: #fff;
  --accent-color: #0679fb;
}
[data-theme="darkMode"] {
  --background-color: #141c30;
  --text-color: #fff;
  --cards-color: #1f2a48;
}
html,
body {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
#app {
  font-family: "Rokkitt", serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  background-color: var(--background-color);
  color: var(--text-color);
  padding: 60px 0;
  height: 100vh;
  overflow: hidden;
  transition: all 800ms;
}
h1 {
  padding: 0;
  margin: 0;
}
.head {
  display: flex;
  flex-flow: row nowrap;
  justify-content: space-around;
  align-items: center;
}
.toggle {
  display: flex;
  flex-flow: row nowrap;
  gap: 12px;
  align-items: flex-end;
  .dark-light {
    text-transform: uppercase;
    font-weight: 500;
  }
  .dark-light--icon {
    width: 18px;
    height: 18px;
    color: var(--text-color);
    transition: 250ms;
    &:hover {
      transform: scale(1.2);
    }
  }
}
</style>
