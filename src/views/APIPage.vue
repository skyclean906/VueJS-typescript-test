<template>
    <div>
      <strong> API Result </strong> <br/>
      <ul v-if="posts && posts.length">
        <li v-for="post of posts">
          <p><strong>{{post.title}}</strong></p>
          <p>{{post.body}}</p>
        </li>
      </ul>

      <ul v-if="errors && errors.length">
        <li v-for="error of errors">
          {{error.message}}
        </li>
      </ul>
      <button @click="goToHome()"> Go to Home </button>
   </div>
</template>
<script lang="ts">
import Vue from 'vue';
import Component from 'vue-class-component';
import axios from 'axios';

@Component({})
export default class APIPage extends Vue {
  posts = [];
  errors = [] as any;
  mounted() : void {
      console.log("mounted");
  }
  async created() {
    try {
       const response = await axios.get(`http://jsonplaceholder.typicode.com/posts`)
       this.posts = response.data
     } catch (e) {
       this.errors.push(e)
     }
  }
  goToHome() : void {
        this.$router.push({
            name: "home"
        });
  }
}
</script>
<style lang="scss" scoped>

</style>
