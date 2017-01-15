<template>
  <div id="app">
    <h1>Vue User Crud</h1>
    <img src="./assets/logo.png" class="app-logo">
    <search-bar @onSearch="onSearch" />
    <user-list :users="filteredUsers"  @deleteUser="deleteUser" />
    <button class="add-user" @click="isModalOpen=true">Add User</button>
    <modal v-show="isModalOpen" @closeModal="isModalOpen=false" :isFormCompleted="isFormCompleted">
      <template slot="modal-title">Add a New User</template>
      <div slot="modal-body">
        
      </div>
    </modal>
  </div>
</template>

<script>
  import UserList from './components/UserList';
  import SearchBar from './components/SearchBar';
  import Modal from './components/Modal';
  import axios from 'axios';
  import { filter, debounce } from 'lodash/fp';

  export default {
    name: 'app',
    components: {
      UserList,
      SearchBar,
      Modal,
    },
    data() {
      return {
        userSearched: '',
        users: [],
        isModalOpen: false,
        userForm: {
          name: '',
          username: '',
          email: '',
          address: {
            street: '',
            suite: '',
            city: '',
          },
          phone: '',
          company: '',
          website: '',
        },
      }
    },
    computed: {
      filteredUsers: function() {
        return filter(user => user.username.toLowerCase().indexOf(this.userSearched.toLowerCase()) >= 0 )(this.users);
      },
      isFormCompleted: function() {
        return this.checkIfFormCompleted(this.userForm);
      }
    },
    methods: {
      onSearch: function(userSearched) {
        this.userSearched=userSearched;
      },
      deleteUser: function(index) {
        this.users.splice(index, 1);
      },
      checkIfFormCompleted: function(formObj) {
        for(let key in formObj) {
          if (typeof formObj[key] === 'object') {
            this.isFormCompleted(formObj[key]);
          } else {
            if (formObj[key] === '') return false;
          }
        }
        return true;
      },
    },
    mounted: function() {
      axios('http://localhost:3000/users').then(response => { this.users = response.data });
    }
  }
</script>

<style>
.app-logo {
  width: 100px;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

html,
body {
  background: #f1f0f0;
  height: 100%;
}

h1 {
  font-size: 2em;
  font-weight: bold;
}
</style>
