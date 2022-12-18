<template>
<h1>Login</h1>
  <div class="form-group">
    <label>Email</label>
    <input type="email" v-model="email" class="form-control">
  </div>
  <br>
  <div class="form-group">
    <label>Password</label>
    <input type="password" v-model="password" class="form-control">
  </div>
    <br>
  <button @click="login()" type="button" class="btn btn-success">Login</button>
    <router-view></router-view>
</template>

<script>
 import axios from 'axios'
export default {
    data: function() {
      return {
        email: null,
        password: null,
      }
    },
    methods: {
      login() {
      axios.post(`http://127.0.0.1:8000/api/login`, {
        email: this.email,
        password: this.password
      })
      .then(response => {
        if(response.data.token!=null){
          localStorage.setItem( 'token', response.data.token );
          this.$router.push('/reservation');
        }else{
            alert(response.data.message);
        }
        console.log(response.data.message);
      })
      .catch(e => { 
      })
      },
    }
  };
</script>


