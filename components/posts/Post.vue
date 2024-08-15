<template>
  <div class="post">
    <div class="post_title">
      Пост
    </div>
    <div class="title">
      <b>Заголовок: </b>{{post.title}}
    </div>
    <div class="body">
      <b>Текст: </b>{{post.body}}
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
  post:{
    type: Object
  }
})

</script>

<style lang="scss" scoped>
.post{
  background-color: rgba(179, 227, 80, 0.5);
  padding: 20px;
  border-radius: 20px;
  margin-top: 30px;
}

.post_title{
  text-align: center;
  font-weight: bold;
  font-size: 22px;
}

.post {
  .body,.title{
    margin-top: 15px;
  }
}
</style>
