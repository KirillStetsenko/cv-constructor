<template>
  <div>
    <div class="container">
      <div class="block1">
        <div class="selectTitle">Block type</div>
        <select id="select" v-model="textType">
          <option value="title">Title</option>
          <option value="subTitle">SubTitle</option>
          <option value="text">Text</option>
          <option value="img">Image</option>
        </select>
        <div class="textareaValue">Value</div>
        <textarea
          id="textarea"
          cols="25"
          rows="3"
          v-model="textareaInput"
          :placeholder="placeholderText"
        ></textarea>

        <button id="btn" @click="textareaInputHandle">Add</button>
      </div>
      <div class="block2">
        <div class="content" v-html="this.textareaOutput"></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      textareaInput: "",
      textareaOutput: "",
      placeholderText: "Enter Title",
      textType: "title",
    };
  },

  watch: {
    textType() {
      switch (this.textType) {
        case "title":
          this.placeholderText = "Enter Title";
          break;
        case "subTitle":
          this.placeholderText = "Enter Subtitle";
          break;
        case "text":
          this.placeholderText = "Enter description";
          break;
        case "img":
          this.placeholderText = "Enter image URL";
          break;
      }
    },
  },

  methods: {
    textareaInputHandle() {
      if (this.textareaInput) {
        switch (this.textType) {
          case "title":
            this.textareaOutput +=
              "<div class='title'>" + this.textareaInput + "</div>";
            this.textareaInput = "";
            break;

          case "subTitle":
            this.textareaOutput +=
              "<div class='subTitle'>" + this.textareaInput + "</div>";
            this.textareaInput = "";
            break;

          case "text":
            this.textareaOutput +=
              "<div class='text'>" + this.textareaInput + "</div>";
            this.textareaInput = "";
            break;

          case "img":
            this.textareaOutput += `<div class='img'><img src='${this.textareaInput}' width=100></div>`;
            this.textareaInput = "";
            break;
        }
      }
    },
  },
};
</script>

<style lang="scss">
$primary-color: rgb(41, 143, 70);
$subtitle-color: rgb(34, 114, 57);
$text-color: #000;
$background-color: white;
$border-radius: 10px;

.border-box {
  border-radius: $border-radius;
  padding: 10px;
}

.container {
  display: flex;
  margin: 10px auto;
  padding: 10px;
  width: min-content;
  border-radius: 20px;

  .block1 {
    margin-right: 20px;
    padding: 20px;
    width: 20%;
    min-width: 200px;
    text-align: center;
    border-radius: 12px;
    background: $background-color;

    .selectTitle {
      text-align: left;
      margin: 5px;
    }

    #select {
      display: block;
      width: 100%;
      border-radius: $border-radius;
      padding: 5px;

      option {
        background: #d4d4d4;
      }
    }

    .textareaValue {
      text-align: left;
      margin: 5px;
    }

    #textarea {
      width: 90%;
      padding: 10px;
      border-radius: $border-radius;
    }

    #btn {
      display: block;
      width: 100%;
      margin-top: 5px;
      padding: 5px;
      border: none;
      border-radius: $border-radius;
      background: $primary-color;
      font-weight: bold;
      color: $background-color;
      transition: background 0.3s ease;

      &:hover {
        background: darken($primary-color, 10%);
      }
    }
  }

  .block2 {
    width: 1000px;
    border-radius: 12px;
    background: $background-color;

    .content {
      box-sizing: border-box;
      padding: 10px;
      width: 100%;
      overflow-wrap: break-word;
    }
  }
}

.title,
.subTitle,
.text {
  @extend .border-box;
  text-align: center;
}

.title {
  color: $primary-color;
  font-size: 26px;
  font-weight: bold;
}

.subTitle {
  color: $subtitle-color;
  font-size: 20px;
  font-weight: bold;
}

.text {
  text-align: justify;
}

.img {
  display: flex;
  justify-content: center;
  margin: 10px;

  img {
    border: 1px solid $text-color;
    border-radius: 50%;
  }
}
</style>
