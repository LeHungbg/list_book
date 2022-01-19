<template>
  <div id="listUser">
    <!-- Hiển thị listbook  -->
    <table v-if="run == true">
      <tr>
        <td><b>Title</b></td>
        <td><b>Isbn13</b></td>
      </tr>
      <tr v-for="(item, index) in info" :key="index">
        <td>
          <a class="link" @click="selectbook(item)">{{ item.title }}</a>
        </td>
        <td>{{ item.isbn13 }}</td>
        <button class="button1" type="submit" @click="deletebook(index)">
          Delete
        </button>
      </tr>
    </table>
    <div>
      <!-- Hiển thị nút thêm và form input thêm -->
      <div v-if="checkAddbook == false">
        <button class="button" type="submit" @click="addbook()">Add</button>
      </div>
      <div v-if="checkAddbook == true">
        <h1>Add book into list</h1>
        <table>
          <tr>
            <td>Link img:</td>
            <td><input v-model="book_image" type="text" /></td>
          </tr>
          <tr>
            <td>Isbn13:</td>
            <td><input v-model="book_isbn13" type="text" /></td>
          </tr>
          <tr>
            <td>Title:</td>
            <td><input v-model="book_title" type="text" /></td>
          </tr>
          <tr>
            <td>Subtitle:</td>
            <td><input v-model="book_subtitle" type="text" /></td>
          </tr>
          <tr>
            <td>Url:</td>
            <td><input v-model="book_url" type="text" /></td>
          </tr>
          <tr>
            <td>Price:</td>
            <td><input v-model="book_price" type="text" /></td>
          </tr>
        </table>
        <div class="button_all">
          <button class="button" type="submit" @click="Saveaddbook()">
            add book
          </button>
          <button class="button2" type="submit" @click="SaveCancel()">
            cancel
          </button>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  data() {
    return {
      info: null,
      isActive: false,
      run: true,
      checkAddbook: false,
      Object: {
        image: null,
        isbn13: null,
        price: null,
        subtitle: null,
        title: null,
        url: null,
      },

      book_image: null,
      book_isbn13: null,
      book_price: null,
      book_subtitle: null,
      book_title: null,
      book_url: null,
    };
  },
  //call api
  created() {
    axios
      .get("https://api.itbook.store/1.0/new")
      .then((response) => (this.info = response.data.books));
  },
  methods: {
    //emit khi chọn vào tile của quyển sách phần detail hiển thị chi tiết quyển sách đc chọn
    selectbook(item) {
      this.$emit("bookSelected", item, this.isActive);
    },
    // delete book
    deletebook(index) {
      this.info.splice(index, 1);
      console.log(index);
      this.$emit("checkdelete", this.isActive);
    },
    // check khi ấn nút add sẽ hiển thị form input
    addbook() {
      this.checkAddbook = true;
    },
    // save book
    Saveaddbook() {
      this.checkAddbook = false;
      this.Object.image = this.book_image;
      this.Object.isbn13 = this.book_isbn13;
      this.Object.price = "$" + this.book_price;
      this.Object.subtitle = this.book_subtitle;
      this.Object.title = this.book_title;
      this.Object.url = this.book_url;
      this.info.push(this.Object);
      console.log(this.Object);
    },
    SaveCancel() {
      this.checkAddbook = false;
    },
  },
};
</script>
<style>
.link:hover {
  color: rgb(255, 1, 1);
}
.button_all {
  display: flex;
  flex-direction: row;
  width: 200px;
  height: 50px;
}
.button1:hover {
  color: rgb(255, 1, 1);
}
.button:hover {
  color: rgb(255, 1, 1);
}
.button2:hover {
  color: rgb(255, 1, 1);
}
.button {
  width: 50px;
  height: 50px;
  margin-left: 60px;
  border-radius: 50px;
  border: none;
  box-shadow: rgba(50, 50, 93, 0.25) 0px 50px 100px -20px,
    rgba(0, 0, 0, 0.3) 0px 30px 60px -30px,
    rgba(10, 37, 64, 0.35) 0px -2px 6px 0px inset;
  box-sizing: border-box;
}
.button2 {
  width: 50px;
  height: 50px;
  margin-left: 10px;
  border-radius: 50px;
  border: none;
  box-shadow: rgba(50, 50, 93, 0.25) 0px 50px 100px -20px,
    rgba(0, 0, 0, 0.3) 0px 30px 60px -30px,
    rgba(10, 37, 64, 0.35) 0px -2px 6px 0px inset;
}
</style>