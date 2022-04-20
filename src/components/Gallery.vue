<template>
  <div class="gallery-box">
    <h1>Test App</h1>
    <div class="gallery">
      <img
        class="gallery-item"
        v-for="item in imgArrLinks"
        :src="item.url"
        :key="item.id"
        :alt="item.id"
        @click="createModal(item.id)" 
      />
    </div>
    <Modal :imgId='targetImgId' v-if="modalShow" @closeModal="closeModal" />
  </div>
</template>

<script>
import Modal from "./Modal";

export default {
  name: "Gallery",
  components: {
    Modal,
  },

  data() {
    return {
      imgArrLinks: [],
      targetImgId: null,
      modalShow: false,
    };
  },

  methods: {
    createModal(id) {
      this.modalShow = true;
      this.targetImgId = id;
      console.log(this.targetImgId);
    },

    closeModal() {
      this.modalShow = false;
    },

   
  },

  beforeMount() {
    this.imgArrLinks = fetch(
      "https://boiling-refuge-66454.herokuapp.com/images"
    )
      .then((response) => response.json())
      .then((data) => (this.imgArrLinks = data));
  },
};
</script>

<style scoped lang="scss">
.gallery-box {
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

    &:hover {
      cursor: pointer;
    }
  }

  @media (max-width: 768px) {
    & {
      justify-content: space-evenly;
    }
  }

  @media (max-width: 640px) {
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
