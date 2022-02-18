<template>
  <div class="modal-box">
    <h1>Test App</h1>
    <div class="gallery">
      <img
        class="gallery-item"
        v-for="item in imgArrLinks"
        :src="item.url"
        :key="item.id"
        alt="img"
        @click="getArg(item.id)"
      />
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data() {
    return {
      imgArrLinks: [],
    };
  },

  methods: {
    getArg(id) {
      this.$emit('getId', id);
      console.log(id, 'from modal screen');
    },
  },

  mounted() {
    this.imgArrLinks = fetch(
      "https://boiling-refuge-66454.herokuapp.com/images"
    )
      .then((response) => response.json())
      .then((data) => (this.imgArrLinks = data));

    console.log(this.imgArrLinks);
  },
};
</script>

<style scoped lang="scss">
.modal-box {
  max-width: 728px;
  margin: 0 auto;
}

h1 {
  margin-bottom: 30px;
  text-align: center;
  font-size: 36px;
  line-height: 42px;
}
.gallery {
  display: flex;
  width: 100%;
  flex-wrap: wrap;
  row-gap: 20px;
  justify-content: space-between;
  align-items: center;
  &-item {
    width: 229px;
  }

  @media (max-width: 687px) {
    & {
      justify-content: center;

      &-item {
        width: 280px;
        margin-bottom: 20px;
      }
    }
  }
}
</style>
