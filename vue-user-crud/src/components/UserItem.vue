<template>
  <div class="user">
    <div class="user-title">
      {{ user.username }}
    </div>
    <div class="user-body">
      <div class="user-data">{{ user.name }}</div>
      <div class="user-data">{{ getRandomInt(20,50) }}</div>
      <div class="user-data">{{ user.email }}</div>
    </div>
    <button class="user-delete" @click="$emit('onDelete', index)">X</button>
  </div>
</template>

<script>
  export default {
    name: 'user-item',
    props: ['user', 'index'],
    methods: {
      getRandomInt: function(min, max) {
        min = Math.ceil(min);
        max = Math.floor(max);
        return Math.floor(Math.random() * (max - min)) + min;
      }
    }
  }
</script>

<style lang="scss" scoped>
  .user{
    display: inline-block;
    background: white;
    margin-bottom: 10px;
    box-shadow: 0px 2px 5px 1px rgba(0,0,0,0.3);
    width: 250px;
    word-break: normal;
    position: relative;

    &:nth-child(2n-1) {
      @media(min-width: 1024px) {
        margin-right: 25px;
      }
    }

    &:nth-child(3n) {
      @media(min-width: 1280px) {
        margin-right: 0;
      }
    }

    &:last-child {
      margin-right: 0;
    }

    @media(min-width: 1280px) {
      margin-right: 25px;
    }
  }

  .user-delete {
    color: white;
    background: black;
    border-radius: 50px;
    border: 1px solid black;
    outline: none;
    position: absolute;
    top: -7px;
    right: -10px;
    cursor: pointer;
    box-shadow: 0px 1px 2px 1px rgba(0, 0, 0, 0.3);
    transition: 0.3s ease-in-out;

    &:hover {
      transform: scale(1.3);
      background: rgba(100,100,100,1);
      border-color: rgba(100,100,100,1);
    }
  }
</style>