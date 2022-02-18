<template>
  <div id="app">
    <Modal @getId='logId' />

    <footer>
      <div class="line"></div>
      <p class="year"> &copy; {{yearNow }}-{{yearNow + 1}} </p>
    </footer>
  </div>
</template>

<script>
import Modal from "./components/Modal";

export default {
  name: "App",
  components: {
    Modal,
  },
  data() {
    return {
      yearNow: new Date().getFullYear(),
    }
  },
  methods: {
    logId(id) {
        console.log(id, 'from app vue')
    }
  }
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

html,
body {
  height: 100%;
  padding: 15px 20px 10px;
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
