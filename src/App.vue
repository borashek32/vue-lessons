<template>
  <div class="app">
    <h3>Posts list</h3>

    <div class="app__btns">
      <my-button
        @click="showDialog"
        >
        Create post
      </my-button>

      <my-input
        v-model="searchQuery"
        type="text"
        placeholder="Search"
        ></my-input>

      <my-select
        v-model="selectedSort"
        :options="sortOptions"
        ></my-select>
    </div>

    <my-dialog 
      v-model:show="dialogVisible"
      >
      <post-form 
        @create="createPost"
        />
    </my-dialog>
    
    <post-list 
      :posts="sortedAndSearchedPosts" 
      @remove="removePost"
      v-if="!isPostsLoading"
      />
    <div v-else>Loading...</div>

    <div class="page__wrapper">
      <div 
        v-for="pageNumber in totalPages" 
        :key="pageNumber"
        class="page"
        :class="{
        'current-page': page === pageNumber  
        }"
        @click="changePage(pageNumber)"
        >
        {{ pageNumber }}
      </div>
    </div>
  </div>
</template>

<script>
import PostList from './components/PostList'
import PostForm from './components/PostForm'
import axios from 'axios'

export default {
  components: {
    PostList, 
    PostForm
  },
  data() {
    return {
      posts: [],
      dialogVisible: false,
      isPostsLoading: false,
      selectedSort: '',
      searchQuery: '',
      page: 1,
      limit: 10,
      totalPage: 0,
      sortOptions: [
        {
          value: 'title',
          name: 'By title'
        },
        {
          value: 'body',
          name: 'By description'
        }
      ]
    }
  },
  methods: {
    createPost(post) {
      this.posts.push(post)
      this.dialogVisible = false
    },
    removePost(post) {
      this.posts = this.posts.filter(p => p.id !== post.id)
    },
    showDialog() {
      this.dialogVisible = true
    },
    changePage(pageNumber) {
      this.page = pageNumber
      this.fetchPosts()
    },
    async fetchPosts() {
      try {
        this.isPostsLoading = true
        setTimeout( async() => {
          const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
            params: {
              _page: this.page,
              _limit: this.limit
            }
          })
          this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit)
          this.posts = response.data
          this.isPostsLoading = false
        }, 1000)
      } catch(e) {
        alert('Error...')
      } 
    }
  },
  mounted() {
    this.fetchPosts()
  },
  computed: {
    sortedPosts() {
      return [...this.posts].sort( (post1, post2,) => {
        return post1[this.selectedSort]?.localeCompare(post2[this.selectedSort])
      })
    },
    sortedAndSearchedPosts() {
      return this.sortedPosts.filter(post => post.title.toLowerCase().includes(this.searchQuery.toLowerCase()))
    }
  },
  watch: {
    
  }
}
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  margin: 0;
}

.app {
  padding: 15px;
}

.app__btns {
  margin: 15px 0;
  display: flex;
  justify-content: space-between;
}

.page__wrapper {
  display: flex;
  justify-content: end;
  margin-top: 15px;
}

.page {
  border: 1px solid teal;
  padding: 10px;
  cursor: pointer;
}

.current-page {
  border: 2px solid teal;
}
</style>