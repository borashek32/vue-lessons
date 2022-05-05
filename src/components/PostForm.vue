<template>
  <div>
    <form @submit.prevent>
      <h4>Create post</h4>
      <my-input 
        v-model="post.title"
        type="text" 
        placeholder="Title"
      ></my-input>
      <my-input 
        v-model="post.body"
        type="text" 
        placeholder="Description"
      ></my-input>
      <my-button 
        @click="createPost"
      >
        Save
      </my-button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      post: {
        title: '',
        body: ''
      }
    }
  },
  methods: {
    createPost() {
      this.post.id = Date.now();
      this.$emit('create', this.post)
      this.post = {
        title: '',
        body: ''
      }
    }
  }
}
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
}

h4 {
  margin-block-start: 0;
  margin-block-end: 0;
  margin-inline-start: 0;
  margin-inline-end: 0;
  margin-bottom: 10px;
}
</style>