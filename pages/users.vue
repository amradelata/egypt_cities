<template>
  <div class="users">
    <section class="hero is-primary">
      <div class="hero-body">
        <div class="container">
          <h1 class="title">صفحه العملاء</h1>
        </div>
      </div>
    </section>

    <div class="container">
      <ul>
        <li v-for="(user,index) in myUsers" class="box cards" :key="user.id">
          <label>user Email:</label>
          <br />
          {{user.userEmail}}
          <br />
          <label>user Password:</label>
          <br />
          {{user.userPassword}}
          <br />
          <button class="button is-danger" @click="deleteUser(index=user.id)">Delete user</button>
        </li>
      </ul>
    </div>
  </div>
</template>


<script>
import axios from "axios";
import { async } from "q";
const usersData = "https://egypt-database.herokuapp.com/users";

export default {
  data() {
    return {
      myUsers: []
    };
  },
  async created() {
    const res = await axios.get(usersData);
    this.myUsers = res.data;
  },
  methods: {
    async deleteUser(index) {
      const res = await axios.delete(usersData + "/" + index);
      const dele = await axios.get(usersData);
      this.myUsers = dele.data;
      console.log(dele);
    }
  }
};
</script>
<style scoped>
.cards {
  margin-top: 50px;
}
</style>
