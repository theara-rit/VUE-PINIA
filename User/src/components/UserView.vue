
<template>
  <main>
    <h2>The Team managment using pinia</h2>
    <form @submit.prevent="CreateUser">
        <div class="form-group">
          <input type="text" placeholder="Name" v-model="user_input.name" class="form-control" required="true">
        </div>
        <div class="form-group">
          <input type="email" placeholder="Email" v-model="user_input.email" class="form-control" required="ture">
        </div>
        <div class="form-group">
          <input type="submit" vlaue="create user" class="btn-form">
        </div>
    </form>
    <div class="sort">
      <span>Sort</span><input type="checkbox" v-model="sort">
    </div>
    <div class="card" v-if="!sort">
      <ul v-for="user of user_store.users" class="user" :key="user">
          <div class="user-info">
            <li>Name: {{user.name}}</li>
            <li>Email: {{user.email}}</li>
          </div>
          <div class="user-action">
            <button @click="DeleteUser(user.id)">Delete</button>
          </div>
      </ul>
    </div>
    <div class="card" v-else>
      <ul v-for="user of user_store.UserByName" class="user" :key="user">
          <div class="user-info">
            <li>Name: {{user.name}}</li>
            <li>Email: {{user.email}}</li>
          </div>
          <div class="user-action">
            <button @click="DeleteUser(user.id)">Delete</button>
          </div>
      </ul>
    </div>
  </main>
</template>

<script setup>
import { useUserStore } from "../stores/UserStore.js";
import {ref} from "vue";

const user_store = useUserStore();

const user_input = ref({
  name: "",
  email: ""
})
const sort = ref(false);

const CreateUser = ()=>{
    user_store.create(user_input.value)

    user_input.value ={
      name : "",
      email: ""
    }
}
const DeleteUser = id =>{
  if (confirm('Are you sure to delete this user?')) {
    user_store.deleteUser(id)
} 
}
</script>
<style scoped>
h2 {
  background-color: green;
  padding: 20px;
  border-radius: 5px;
  text-align: center;
  color: #fff;
}
form{
  width: 100%;
  box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;
  border-radius: 5px;
  padding: 10px;
  margin: auto;
  box-sizing: border-box;
}
form .form-group{
  width: 95%;
  margin: auto;
  box-sizing: border-box;
  margin-top: 1rem;
  display: flex; 
  justify-content: center;
  align-items: center;
}
form .form-group .form-control{
  padding: 10px;
  width: 100%;
  outline: none;
}
.btn-form{
  width: 100%;
  padding: 10px;
  margin-bottom: 1rem;
  background-color: rgb(49, 125, 240);
  border: none;
  border-radius: 5px;
  color: white;
}
.btn-form:hover{
  background-color: rgb(78, 144, 243);
  border-radius: 5px;
  color: white;
  cursor: pointer;
}
.card ul{
  box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;
  list-style-type: none;
  text-align: left;
  border-radius: 5px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0.5rem;
}
.card ul li{
  list-style-type: none;
}
.user-action button{
  padding: 7px 15px;
  border-radius: 5px;
  background-color: rgb(209, 7, 67);
  border: none;
  color: white;
}
.sort{ 
  box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;
  padding: 7px 15px;
  margin-top: 1rem;
  width: 50px;
  border-radius: 5px;
}
.sort, .sort input:hover{
  cursor: pointer;
}
</style>
