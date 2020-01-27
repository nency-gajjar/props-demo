<template>
  <div>
    <ul v-for="(comment, index) in comments" :key="index">
      <li v-if="seen"><a>{{comment.name}}</a></li>
    </ul>
  </div>
</template>

<script>
import axios from "axios";
const url = "https://jsonplaceholder.typicode.com";
export default {
  name: "postComments",
  props: ["post" , 'seen'],
  data() {
    return {
        comments: []
    }
  },
  mounted() {
      this.getComments(this.post.id)
  },
  methods: {
    async getComments (id) {
      let commentUrl = url + '/comments?postId=' + id
      this.comments = (await axios.get(commentUrl)).data; 
    }
  }
}
</script>