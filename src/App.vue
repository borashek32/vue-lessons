<template>
  <div class="app">
    <form @submit.prevent>
      <h4>Create post</h4>
      <input 
        v-bind:value="title" 
        @input="title = $event.target.value"
        class="input" 
        type="text" 
        placeholder="Title"
      >
      <input 
        v-bind:value="body" 
        @input="body = $event.target.value"
        class="input" 
        type="text" 
        placeholder="Description"
      >
      <button 
        class="btn" 
        @click="createPost"
      >
        Save
      </button>
    </form>

    <div class="post" 
      v-for="post in posts" 
      v-bind:key="post"
    >
      <div>
        <strong>Title:</strong>
        {{ post.title }}
      </div>
      <div>
        <strong>Description:</strong>
        {{ post.body }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      posts: [
        {id: 1, title: 'Post1', body: 'description1'},
        {id: 2, title: 'Post2', body: 'description2'},
        {id: 3, title: 'Post3', body: 'description3'}
      ],
      title: '',
      body: '',
    }
  },
  methods: {
    createPost() {
      const newPost = {
        id: Date.now(),
        title: this.title,
        body: this.body
      }
      this.posts.push(newPost);
      this.title ='';
      this.body = '';
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

.post {
  padding: 15px;
  border: 2px solid teal;
  margin-top: 15px;
}

form {
  display: flex;
  flex-direction: column;
}

.btn {
  align-self: flex-end;
  margin-top: 15px;
  padding: 10px 15px;
  background: none;
  color: teal;
  border: 1px solid teal;
}

.input {
  width: 100%;
  border: 2px solid teal;
  padding: 10px 15px;
  margin-top: 15px;
}
</style>