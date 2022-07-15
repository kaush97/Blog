<template>
  <v-card class="mx-auto">
    <v-list three-line>
      <v-subheader :key="index">All Blogs</v-subheader>
      <template v-for="(item, index) in items">
        <v-divider :key="index"></v-divider>

        <v-list-item :key="index">
          <v-list-item-avatar>
            <v-img src="../assets/blog.png"></v-img>
          </v-list-item-avatar>

          <v-list-item-content>
            <v-list-item-title
              class="black--text"
              v-html="item.title"
            ></v-list-item-title>
            <v-list-item-subtitle v-html="item.subTitle"></v-list-item-subtitle>
          </v-list-item-content>
          <v-btn @click="openBlog(item)">show</v-btn>

          <v-btn @click="EditBlog(item)" class="ms-2"
            ><v-icon>mdi-pencil</v-icon></v-btn
          >

          <v-btn @click="DeleteBlog(item)" class="ms-2"
            ><v-icon>mdi-delete</v-icon>
          </v-btn>
        </v-list-item>
      </template>
    </v-list>
  </v-card>
</template>
<script>
export default {
  data: () => ({
    items: [],
  }),
  methods: {
    openBlog(item) {
      this.$router.push("/blog-details/" + item.id);
    },
    EditBlog(item) {
      this.$router.push("/edit-blog/" + item.id);
    },
    DeleteBlog(item) {
      debugger;
      this.$store.dispatch("deleteBlog", item);
    },
  },
  created() {
    let a = this.$store.state.blogs;
    this.items = a.filter(
      (item) => item.createdBy == this.$store.state.username
    );
    console.log(this.items);
  },
};
</script>
