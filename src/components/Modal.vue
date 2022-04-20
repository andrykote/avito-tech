<template>
  <div class="modal" @click="closeModal">
    <div class="modal-container">
      <div class="modal-svg-box">
        <svg
        @click="closeModal"
          width="20"
          height="19"
          viewBox="0 0 20 19"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <line
            x1="1.35355"
            y1="0.646447"
            x2="19.3536"
            y2="18.6464"
            stroke="black"
          />
          <line
            x1="0.646447"
            y1="18.6464"
            x2="18.6464"
            y2="0.646446"
            stroke="black"
          />
        </svg>
      </div>
      <div class="modal-section">
        <img class="modal-img" :src="url" alt="img" />

        <div class="modal-comment" v-if="comments.length === 0">
          <p>Нет комментариев</p>
        </div>
        <div
          class="modal-comment"
          v-else
          v-for="(comment, index) in comments"
          :key="index"
        >
          <p class="modal-comment-date">
            {{ transformDate(comments[index].date) }}
          </p>
          <p class="modal-comment-text">{{ comments[index].text }}</p>
        </div>
      </div>

      <form class="modal-form" action="" method="post">
        <input class="modal-form-input" type="text" placeholder="Ваше имя" />
        <input
          class="modal-form-input"
          type="text"
          placeholder="Ваш комментарий"
        />
        <button class="modal-form-button" type="submit">
          Оставить комментарий
        </button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: "Modal",
  props: {
    imgeId: Number,
  },

  data() {
    return {
      url: null,
      comments: [],
    };
  },

  methods: {
    closeModal(event) {
      if (!event.target.closest(".modal-container") || event.target.closest(".modal-svg-box")) {
        this.$emit("closeModal", false);
      }
    },

    transformDate(inputDate) {
      return new Date(inputDate).toLocaleDateString();
    },
  },

  beforeMount() {
    fetch(`https://boiling-refuge-66454.herokuapp.com/images/${this.imgeId}`)
      .then((data) => data.json())
      .then((item) => {
        this.url = item.url;
        this.comments = item.comments;
        console.log(this.comments);
      });
  },
};
</script>

<style lang="scss" scoped>
.modal {
  position: absolute;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100vw;
  height: 100vh;
  top: 0;
  left: 0;
  z-index: 1;
  background-color: rgba(0, 0, 0, 0.6);
  font-size: 13px;

  &-container {
    position: relative;
    display: flex;
    flex-direction: column;
    width: 662px;
    padding: 30px;
    background-color: #fff;
  }

  &-section {
    display: flex;
  }

  &-svg-box {
      position: absolute;
      width: 18px;
      height: 18px;
      right: 21px;
      top: 21px;
      cursor: pointer;
  }

  &-img {
    max-width: 332px;
    margin-right: 14px;
    margin-bottom: 30px;
  }

  &-comment {
    width: 100%;
    text-align: left;
    margin-bottom: 20px;

    &-date {
      color: #999;
      margin-bottom: 5px;
    }
  }

  &-form {
    display: flex;
    flex-direction: column;
    max-width: 332px;
    row-gap: 20px;

    &-input,
    &-button {
      padding: 8px 11px 7px;
      border-radius: 3px;
    }

    &-input {
      border: 1px solid #ccc;
    }

    &-button {
      background-color: #4997d0;
      color: #fff;
      border: none;
      cursor: pointer;
    }
  }
}
</style>
