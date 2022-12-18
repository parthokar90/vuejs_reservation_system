<template>
<h4>Room and Suites</h4>
<div class="row">
    <div v-for="(room,key) in rooms" :key="key" class="col-md-3">
      <div class="card" style="width:100%">
  <img class="card-img-top" v-bind:src="room.photo" alt="Card image">
  <div class="card-body">
    <h5 class="card-title" style="color:#000000">{{room.name}} </h5>
    <p class="card-text" style="color:#000000">Room Size:{{room.size}}</p>
    <p class="card-text" style="color:#000000">Price:{{room.price}}</p>
    <p class="card-text" style="color:#000000">{{room.description}}</p>
    <button @click="bookNow" class="btn btn-warning">Book Now</button>
  </div>
</div>
    </div>
</div>
</template>

<script>
 import axios from 'axios'
export default {
    name:"rooms",
    data(){
        return {
            rooms:[]
        }
    },
    mounted(){
        this.getRooms()
    },
    methods:{
         getRooms(){
             axios.get(`http://127.0.0.1:8000/api/room`).then(response=>{
                this.rooms = response.data
                console.log(response);
            }).catch(error=>{
                console.log(error)
                this.rooms = []
            })
        },
        bookNow(){
          let token = localStorage.getItem('token');
          if(token==null){
              this.$router.push('/login');
          }else{
            this.$router.push('/reservation');
          }
        }
    }
}
</script>

