<template>
  <div class="app">
    <h3>Posts list</h3>

    <my-button
      style="margin:15px 0"
      @click="showDialog"
    >
      Create post
    </my-button>

    <my-dialog v-model:show="dialogVisible">
      <post-form 
        @create="createPost"
      />
    </my-dialog>
    
    <post-list 
      :posts="posts" 
      @remove="removePost"
    />
  </div>
</template>

<script>
import PostList from './components/PostList'
import PostForm from './components/PostForm'

export default {
  components: {
    PostList, 
    PostForm
  },
  data() {
    return {
      posts: [
        {id: 1, title: 'Post1', body: 'description1'},
        {id: 2, title: 'Post2', body: 'description2'},
        {id: 3, title: 'Post3', body: 'description3'}
      ],
      dialogVisible: false
    }
  },
  methods: {
    createPost(post) {
      this.posts.push(post);
      this.dialogVisible = false;
    },
    removePost(post) {
      this.posts = this.posts.filter(p => p.id !== post.id);
    },
    showDialog() {
      this.dialogVisible = true;
    }
  }
}
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.app {
  padding: 15px;
}

body {
  margin: 0;
}
</style>