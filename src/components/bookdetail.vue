<template>
  <div class="user-detail">
    <!-- Chưa chọn bookdetail sẽ hiển thị text {{information}} -->
    <div class="condition1" v-if="isActive == false">{{ information }}</div>
    <!-- Hiển thị book_detail đc chọn -->
    <div class="condition2" v-if="isActive == true">
      <viewer class="img"
        ><img :src="bookdetail.image" style="height: 100%; with: 100%"
      /></viewer>
      <div><span class="text">Isbn13: </span>{{ bookdetail.isbn13 }}</div>
      <div>
        <!-- check: Khi ấn nút edit đổi title thành form input  -->
        <span class="text">Title: </span
        ><span v-if="checked == true">{{ bookdetail.title }}</span
        ><input
          :placeholder="bookdetail.title"
          v-model="bookdetail_title"
          type="text"
          v-if="checked == false"
        />
      </div>
      <div>
        <!-- check: Khi ấn nút edit đổi Subtitle thành form input  -->
        <span class="text">Subtitle: </span
        ><span v-if="checked == true">{{ bookdetail.subtitle }}</span
        ><input
          :placeholder="bookdetail.subtitle"
          v-model="bookdetail_subtitle"
          type="text"
          v-if="checked == false"
        />
      </div>
      <div>
        <!-- check: Khi ấn nút edit đổi url thành form input  -->
        <span class="text">Url: </span
        ><span v-if="checked == true">{{ bookdetail.url }}</span
        ><input
          :placeholder="bookdetail.url"
          v-model="bookdetail_url"
          type="text"
          bookdetail_subtitle
          v-if="checked == false"
        />
      </div>
      <div>
        <!-- check: Khi ấn nút edit đổi Price  thành form input  -->
        <span class="text">Price: </span
        ><span v-if="checked == true">{{ bookdetail.price }}</span
        ><input
          :placeholder="bookdetail.price"
          v-model="bookdetail_price"
          type="text"
          v-if="checked == false"
        />
      </div>
      <!-- Chọn nút edit hiển thị nút save & nút cancel -->
      <button
        v-if="checksave == false"
        class="button"
        type="submit"
        @click.prevent="check()"
      >
        Edit
      </button>
      <button
        v-if="checksave == true"
        class="button"
        type="submit"
        @click.prevent="cancel()"
      >
        cancel
      </button>
      <button
        v-if="checksave == true"
        class="button"
        type="submit"
        @click.prevent="save()"
      >
        save
      </button>
    </div>
  </div>
</template>
<script>
export default {
  components: {},
  props: {
    //nhận từ app.vu (cha)
    bookdetail: {
      type: Object,
    },
    isActive: {
      type: Boolean,
    },
    check1: {
      type: Boolean,
    },
  },
  data() {
    return {
      checked: true,
      information: "nothing",
      id: null,
      checksave: false,
      bookdetail_subtitle: this.bookdetail.subtitle,
    };
  },
  methods: {
    check() {
      this.checked = false;
      this.checksave = true;
    },
    cancel() {
      this.checked = true;
      this.checksave = false;
    },
    save() {
      this.id = this.bookdetail.isbn13;
      (this.bookdetail.subtitle = this.bookdetail_subtitle),
        (this.bookdetail.url = this.bookdetail_url),
        (this.bookdetail.price = "$" + this.bookdetail_price);
      this.checked = true;
      this.checksave = false;
    },
  },
};
</script>
<style scoped>
.condition2 {
  color: rgb(38, 0, 255);
}
.text {
  width: 60px;
  color: black;
  display: inline-block;
}
.button {
  width: 50px;
  height: 50px;
  margin-left: 5px;
  border-radius: 50px;
  border: none;
  box-shadow: rgba(50, 50, 93, 0.25) 0px 50px 100px -20px,
    rgba(0, 0, 0, 0.3) 0px 30px 60px -30px,
    rgba(10, 37, 64, 0.35) 0px -2px 6px 0px inset;
}
</style>
