<template>
  <div>
    <!-- <div 
      v-if="posts.lenght > 0"
      style="color:red;margin-top:15px"
    > -->
    <div>
      <post-item
        v-for="post in posts" 
        :post="post"
        :key="post.id"
        @remove="$emit('remove', post)"
    /></div>

    <!-- <div 
      v-else
      style="color:red;margin-top:15px"
    >
      <h3>
        Posts list is empty
      </h3>
    </div> -->
  </div>
</template>

<script>
import PostItem from '@/components/PostItem'

export default {
  components: {
    PostItem
  },
  props: {
    posts: {
      type: Array,
      required: true
    }
  }
}
</script>

<style scoped>

</style>