<template>
  <div class="modal" @click="closeModal">
    <div class="modal-container">
      <img class="modal-img" :src="url" alt="img" />
      <div
        class="modal-comment"
        v-for="(comment, index) in comments"
        :key="index"
      >
        <p>{{ comments[index].text }}</p>
        <p>{{ comments[index].date }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Modal",
  props: {
    imgId: Number,
  },

  data() {
    return {
      url: null,
      comments: [],
    };
  },

  methods: {
    closeModal(event) {
      if (!event.target.closest(".modal-container")) {
        this.$emit("closeModal", false);
      }
    },
  },

  beforeMount() {
    fetch(`https://boiling-refuge-66454.herokuapp.com/images/${this.imgId}`)
      .then((data) => data.json())
      .then((item) => {
        this.url = item.url;
        this.comments = item.comments;
      });
  },
};
</script>

<style lang="scss" scoped>
.modal {
  position: absolute;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  z-index: 1;
  background-color: rgba(0, 0, 0, 0.6);

  &-img {
    margin: 0 auto;
  }

  &-comment {
    font-size: 20px;
  }
}
</style>
