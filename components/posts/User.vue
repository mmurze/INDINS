<template>
  <div class="user">
    <div class="user_title">
      Создатель поста
    </div>
    <div class="text">
      <p class="text_title">
        Имя:
      </p>
      <div class="name">
        {{user.name}}
      </div>
    </div>
    <div class="text">
      <p class="text_title">
        Никнейм:
      </p>
      <div class="name">
        {{user.username}}
      </div>
    </div>
    <div class="text">
      <p class="text_title">
        Почта:
      </p>
      <div class="name">
        {{user.email}}
      </div>
    </div>
    <div class="text">
      <p class="text_title">
        Адрес:
      </p>
      <div class="name">
        {{user.address.street}} {{user.address.suite}} {{user.address.city}} {{user.address.zipcode}}
      </div>
    </div>
    <div class="text">
      <p class="text_title">
        Телефон:
      </p>
      <div class="name">
        {{user.phone}}
      </div>
    </div>
    <div class="text">
      <p class="text_title">
        Сайт:
      </p>
      <div class="name">
        {{user.website}}
      </div>
    </div>
    <div class="text">
      <p class="text_title">
        Компания:
      </p>
      <div class="name">
        {{user.company.name}}
      </div>
    </div>
  </div>
</template>

<script setup>

const props = defineProps({
  user:{
    type: Object
  }
})


</script>

<style lang="scss" scoped>
.user{
  background-color: rgba(179, 227, 80, 0.5);
  padding: 20px;
  border-radius: 20px;
  margin-top: 30px;
}

.user_title{
  text-align: center;
  font-weight: bold;
  font-size: 22px;
}

.text{
  display: flex;
  gap: 15px;
  margin-top: 10px;
  .text_title{
    font-weight: bold;
  }
  &:first-child{
    margin-top: 0;
  }
}
</style>
