<template>
  <div class="users">
    <user-item 
      v-for="(user, index) in users"
      :user="user"
      :index="index"
      @onDelete="(index) => { $emit('deleteUser', index) }" />
  </div>
</template>

<script>
  import UserItem from './UserItem';

  export default {
    name: 'user-list',
    props: ['users'],
    components: {
      UserItem,
    },
  }
</script>

<style lang="scss" scoped>
  .users {
    margin: 0 auto;
    max-width: 300px;

    @media(min-width: 1024px) {
      max-width: 600px;
    } 

    @media(min-width: 1280px) {
      max-width: 900px;
    }
  }
</style>