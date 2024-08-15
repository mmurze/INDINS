<template>
  <div class="">
    <div class="select_container">
      <select v-model="selectedUser" class="select">
        <option selected value="0">
          Выберите пользователя
        </option>
        <option v-for="user in users" :key="user.id" :value="user.id">
          {{user.name}}
        </option>
      </select>
    </div>
    <div class="posts">
      <div
          v-for="post in filterPosts"
          :key="post.id"
          class="post"
          @click="toPost(post.id)"
      >
        <p class="name_title">
          Заголовок:
        </p>
        <p class="title">
          {{post.title}}
        </p>
      </div>
    </div>
  </div>
</template>

<script setup>
import {ref, computed} from "vue";
import {navigateTo, useFetch} from "nuxt/app";

const selectedUser = ref('0')

const posts = await useFetch('https://jsonplaceholder.typicode.com/posts').data
const users = await useFetch('https://jsonplaceholder.typicode.com/users').data

const filterPosts = computed(() => {
  if(selectedUser.value !== '0'){
    return posts.value.filter(item => item.userId === selectedUser.value)
  }
  return posts.value
})

function toPost(id){
  navigateTo(`/posts/${id}`)
}

</script>

<style scoped>
.select_container{
}
.select{
  margin: 10px auto;
  display: flex;
  padding: 10px;
  font-size: 17px;
  width: 50%;
}
.posts{
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 25px;
  justify-content: center;
}
.post{
  padding: 10px 20px;
  border-radius: 10px;
  background-color: rgba(179, 227, 80, 0.5);
  cursor: pointer;
}
.name_title{
  font-weight: bold;
}

@media (max-width: 600px) {
  .select{
    width: 90%;
  }
  .posts{
    grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
    gap: 15px;
  }
}
</style>
