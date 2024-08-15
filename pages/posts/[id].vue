<template>
  <div v-if="!(post && user && comments)">
    Загрузка
  </div>
  <div v-else class="info_container">
    <button @click="navigateTo('/')">
      back
    </button>
    <PostsUser :user="user"/>
    <PostsPost :post="post"/>
    <form class="add_comment">
      <div class="add_comment_title">
        Оставить отзыв
      </div>
      <div class="input">
        <label for="email" class="input_title">
          Введите почту:
        </label>
        <input type="email" id="email" v-model="inputEmail">
      </div>
      <div class="input">
        <label for="title" class="input_title">
          Введите название:
        </label>
        <input type="text" id="title" v-model="inputName">
      </div>
      <div class="input">
        <p class="input_title">
          Введите комментарий:
        </p>
        <textarea class="body" v-model="inputComment"/>
      </div>
      <div class="button">
        <button
            :class="{disabled: disabledButton}"
            :disabled="disabledButton"
            @click.prevent="addComment"
        >
          Отправить
        </button>
      </div>
    </form>
    <PostsComments :comments="comments"/>
  </div>
</template>

<script setup>
import {navigateTo, useRoute} from "nuxt/app";
import {computed, ref} from "vue";

const route = useRoute()
const postId = route.params.id
const user = ref()
const post = ref()
const comments = ref()

const inputEmail = ref('')
const inputName = ref('')
const inputComment = ref('')


async function getData(){
  post.value = await $fetch(`https://jsonplaceholder.typicode.com/posts/${postId}`, {
    method: 'GET'
  })
  user.value = await $fetch(`https://jsonplaceholder.typicode.com/users/${post.value.userId}`, {
    method: 'GET'
  })
  comments.value = await $fetch(`https://jsonplaceholder.typicode.com/comments?postId=${post.value.userId}`, {
    method: 'GET'
  })
}
getData()

const disabledButton = computed(() => (inputComment.value === '' || inputEmail.value === '' || inputName.value === ''))

function addComment(){
  $fetch(
      `https://jsonplaceholder.typicode.com/comments?postId=${post.value.userId}`, {
        method: 'POST',
        headers: {
          'Content-type': 'application/json; charset=UTF-8',
        },
        body: JSON.stringify({
          "postId": postId,
          "name": inputName.value,
          "email": inputEmail.value,
          "body": inputComment.value
        }),
      }
  )
      .then(res => alert("все успешно отправилось \n" + JSON.stringify(res) ))
      .catch(e => console.error(e))

  inputEmail.value = ''
  inputName.value = ''
  inputComment.value = ''
}

</script>

<style lang="scss" scoped>

button{
  width: 100px;
  padding: 10px 5px;
  font-family: Roboto, sans-serif;
  border: none;
  background-color: rgba(163, 222, 60, 1);
  border-radius: 5px;
  cursor: pointer;
  &.disabled{
    cursor: none;
    background-color: rgb(193, 224, 165);
  }
}

.add_comment{
  background-color: rgba(179, 227, 80, 0.5);
  padding: 20px;
  border-radius: 20px;
  margin-top: 30px;
}

.add_comment_title{
  text-align: center;
  font-weight: bold;
  font-size: 22px;
}

.add_comment{
  display: flex;
  flex-direction: column;
  gap: 15px;
  .button{
    display: flex;
    justify-content: flex-end;
  }
}

.input{
  display: flex;
  gap: 10px;
  .input_title{
    min-width: 20%;
  }
  input{
    width: 100%;
    border: none;
    background-color: rgba(0,0,0, 0);
    border-bottom: 2px solid rgba(163, 222, 60, 1);
    outline: none;
    padding: 4px;
    font-size: 16px;
  }
  textarea{
    width: 100%;
    height: 50px;
    resize: none;
    outline: none;
    background-color: rgba(0,0,0, 0);
    border: 2px solid rgba(163, 222, 60, 1);
    border-radius: 5px;
  }
}

</style>
