<template>
  <div class="comments">
    <div class="comments_title">
      Комментарии
    </div>
    <div
        v-for="comment in comments"
        :key="comment.id"
        class="comment"
    >
      <div class="email">
        {{comment.email}}
      </div>
      <div class="name">
        {{comment.name}}
      </div>
      <div class="body">
        {{comment.body}}
      </div>
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
  comments:{
    type: Array
  }
})
</script>

<style lang="scss" scoped>
.comments{
  background-color: rgba(179, 227, 80, 0.5);
  padding: 20px;
  border-radius: 20px;
  margin-top: 30px;
}

.comments_title{
  text-align: center;
  font-weight: bold;
  font-size: 22px;
}

.comments{
  display: flex;
  flex-direction: column;
  gap: 15px;
}
.comment{
  display: flex;
  flex-direction: column;
  gap: 5px;
  border: 2px solid rgba(163, 222, 60, 1);
  padding: 5px;
  border-radius: 10px;
  .email{
    font-weight: bold;
  }
}
</style>
