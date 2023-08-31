<script setup>
import axios from 'axios';
import { onMounted, ref } from 'vue';

const posts = ref([]);
const categories = ref([]);

onMounted(()=>{
  fetchPosts();
  fetchCategories();
});

async function fetchPosts() {
  let url = 'https://basic-blog.teamrabbil.com/api/post-newest';
  
  let res = await axios.get(url);
  posts.value = res.data;
  }

async function fetchCategories() {
  let url = 'https://basic-blog.teamrabbil.com/api/post-categories';
  let res = await axios.get(url);
  categories.value = res.data;
}
</script>

<template>
  <div>
    <ul class="categories">
      <li v-for="category in categories" :key="category.id">
        <a href="#">{{ category.name }}</a>
      </li>
    </ul>
    <h2>Blog Posts</h2>
      <div v-for="post in posts" :key="post.id">
        <img :src="post.img" alt="" style="max-width: 100%;">
        <h3>{{ post.title }}</h3>
        <p>{{ post.short }}</p>
      </div>
  </div>
</template>

<style scoped>
.categories {
  list-style: none;
}
.categories li{
  display: inline-block;
}
.categories li a {
  padding: 5px 10px;
  background-color: rgb(51, 54, 54);
  color: #fff;
}
</style>