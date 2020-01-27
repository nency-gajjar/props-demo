<template>
  <div>
    <ul v-for="(post,id) in posts" :key="id">
      <a href="javascript:void(0)" @click="seen=!seen">{{post.title}}</a>
      <!-- <span>
        <button @click="showComments(post.id)">Get Comments</button> -->
      <!-- </span> -->
      <post-comments :post="post" :seen='seen'></post-comments>
      <hr />
      <!-- <propsexchild :posts-title="posts.title" :desc="posts.body" :comments="comments" @editparent="editParent()"></propsexchild> -->
    </ul>
  </div>
</template>
<script>
import axios from "axios";
import postComments from "@/components/postComments.vue";
const url = "https://jsonplaceholder.typicode.com";
export default {
  data() {
    return {
      posts: null,
      comments: null,
      seen : false
    };
  },
  components: {
    postComments
  },
  async created() {
    this.posts = await this.getPosts();
  },
  methods: {
    async getPosts() {
      let url1 = url + "/posts";
      return (await axios.get(url1)).data;
    },

    // async getComments() {
    //   return (
    //     await axios.get("https://jsonplaceholder.typicode.com/posts/1/comments")
    //   ).data;
    // },

    // editParent() {
    //   this.$emit("edit");
    //   prompt("are you sure?");
    //   console.log("parent=====edit button click ");
    // },
    
    // async showComments(id) {
    //   //   // alert(id)
    //   let commentUrl = url + "/comments?postId=" + id;
    //   this.comments = (await axios.get(commentUrl)).data;
    // }
  }
};
</script>