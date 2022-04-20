<template>
  <div id="app">
    <Gallery/>

    <footer>
      <div class="line"></div>
      <p class="year"> &copy; {{yearNow }}-{{yearNow + 1}} </p>
    </footer>
  </div>
</template>

<script>
import Gallery from "./components/Gallery";

export default {
  name: "App",
  components: {
    Gallery,
  },
  data() {
    return {
      yearNow: new Date().getFullYear(),
    }
  },
};
</script>

<style lang="scss">
$base-color: #ccc;

* {
  box-sizing: border-box;
  text-decoration: none;
  margin: 0;
  padding: 0;
  font-family: "Roboto", sans-serif;
}

html {
  height: 100%;
  padding: 0;
}
body {
  height: 100%;
  padding: 15px 20px 10px;
}

body {
    position: relative;
}
#app {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 100%;
}

.line {
  max-width: 100%;
  height: 1px;
  margin-bottom: 10px;
  background-color: $base-color;
}

.year {
  width: 100%;
  text-align: center;
  color: $base-color;
}
</style>
