<template>
  <v-row>
    <v-app-bar color="teal" dark app>
      <v-toolbar-title> {{ data[0].title }}</v-toolbar-title>
      <v-spacer></v-spacer>
    </v-app-bar>
    <v-col md="8" class="left-container">
      <v-row justify="space-between" class="mb-5">
        <v-col md="9">
          <v-avatar color="red">
            <span class="white--text text-h5"> {{ data[0].createdBy[0] }}</span>
          </v-avatar>
          <span class="black--text text-body"> {{ data[0].createdBy }}</span>
          <v-col>
            <span class="black--text date"> {{ formatDate }}</span>
          </v-col>
        </v-col>
        <v-col align-self="end" md="3">
          <v-icon large color="gray darken-2"> mdi-facebook </v-icon>
          <v-icon large color="gray darken-2"> mdi-twitter </v-icon>
          <v-icon large color="gray darken-2"> mdi-linkedin </v-icon>
        </v-col>
      </v-row>
      <v-row>
        <v-col>
          <div style="overflow: hidden" v-html="data[0].data"></div>
        </v-col>
      </v-row>
      <v-row>
        <v-col>
          <h5 class="author">created by - {{ data[0].createdBy }}</h5>
        </v-col>
      </v-row>
    </v-col>
    <v-col md="4" class="right-container">
      <v-col md="12">
        <v-avatar color="red">
          <span class="white--text text-h5"> {{ data[0].createdBy[0] }}</span>
        </v-avatar>
      </v-col>
      <v-col md="12">
        <span class="black--text text-body"> {{ data[0].createdBy }}</span>
      </v-col>
      <v-col md="12">
        <v-chip draggable>
          Follow <v-icon large color="gray" small> mdi-plus </v-icon>
        </v-chip>
        <v-col md="12">
          <h3>More...</h3>
          <template v-for="(item, index) in items">
            <v-divider :key="index"></v-divider>

            <v-list-item :key="index" @click="openBlog(item)">
              <v-list-item-avatar>
                <v-img :src="item.avatar"></v-img>
              </v-list-item-avatar>

              <v-list-item-content>
                <v-list-item-title
                  class="black--text"
                  v-html="item.title"
                ></v-list-item-title>
                <v-list-item-subtitle
                  v-html="item.subTitle"
                ></v-list-item-subtitle>
              </v-list-item-content>
            </v-list-item>
          </template>
        </v-col>
      </v-col>
    </v-col>
  </v-row>
</template>
<script>
export default {
  data() {
    return {
      data: "",
      items: [],
    };
  },
  methods: {
    openBlog(item) {
      this.$router.push("/blog-details/" + item.id);
    },
  },
  computed: {
    formatDate() {
      let a = [{ day: "numeric" }, { month: "short" }, { year: "numeric" }];

      function format(m) {
        let f = new Intl.DateTimeFormat("en", m);
        return f.format(this?.data[0]?.createdAt);
      }
      return a.map(format).join("-");
    },
  },
  watch: {
    $route(to, from) {
      console.log(to, from);
      let blogs = this.$store.state.blogs;

      this.data = blogs.filter((item) => item.id == this.$route.params.id);
    },
  },
  created() {
    let blogs = this.$store.state.blogs;
    this.items = blogs.filter(
      (item) => item.createdBy == this.$store.state.username
    );
    let item = blogs.filter((item) => item.id == this.$route.params.id);
    console.log(item, "dafs");
    this.data = item;
  },
};
</script>
<style scoped>
.right-container {
  position: fixed;
  top: 65px;
  right: 0;
  width: 30vw;
  height: 100vh;
  -webkit-box-shadow: -2px -1px 5px -3px rgba(0, 0, 0, 0.75);
  -moz-box-shadow: -2px -1px 5px -3px rgba(0, 0, 0, 0.75);
  box-shadow: -2px -1px 5px -3px rgba(0, 0, 0, 0.75);
  padding-top: 50px;
}
.author {
  text-align: end;
}
.date {
  font-size: 12px;
}
.left-container {
  padding: 4em;
}
</style>
