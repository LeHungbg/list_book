<template>
 <div id="app">
    <div class="book-list">
      <h1>List Book</h1>
      <ListBook
        @bookSelected="childSelected"
      ></ListBook>
    </div>
    <div class="book-detail">
      <h1>Book detail</h1>
      <BookDetail
        :bookdetail="bookSelectedfromchild"
        :isActive="isActive1"
        :checkdeleted="check1"
      ></BookDetail>
    </div>
  </div>
</template>
<script>
import BookDetail from "./components/bookdetail.vue";
import ListBook from "./components/listbook.vue";
export default {
  name: "app",
  components: {
    ListBook,
    BookDetail,
    // test1
  },
  data() {
    return {
      bookSelectedfromchild: {},
      bookUpdatefromchild: {},
      isActive1: false,
      check: false,
    };
  },
  methods: {
    childSelected(item, isActive) {
      console.log(item);
      console.log(isActive);
      this.isActive1 = true;
      this.bookSelectedfromchild = item;
    },
  },
};
</script>
<style lang="scss" scoped>
</style>
