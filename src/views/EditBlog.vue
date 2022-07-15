<template>
  <RichTextEditor :data="data" class="mr-3 ml-3" />
</template>
<script>
import RichTextEditor from "../views/RichTextEditor.vue";

export default {
  data() {
    return {
      data: null,
    };
  },
  components: {
    RichTextEditor,
  },
  created() {
    let blogs = this.$store.state.blogs;

    let item = blogs.filter((item) => item.id == this.$route.params.id);
    console.log(item, "dafs");
    this.data = item;
  },
};
</script>