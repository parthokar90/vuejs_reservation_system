<template>
<h1>Room Reservation</h1>
<p style="color:#000000">User Name:  {{name}} </p><br>

<form>
 <div class="form-group">
   <label>Check In</label>
   <br>
   <input v-model="roomData.checkIn"  type="date">
 </div>

 <br>

  <div class="form-group">
   <label>Check Out</label>
   <br>
   <input v-model="roomData.checkOut" type="date">
 </div>
 <br>
 <button type="button" @click="RoomBookNow" class="btn btn-warning">Book Now</button>
</form>

</template>


 <script>
import axios from "axios";
export default {
  name: "HelloWorld",
  data() {
    return {
      name: '',
      roomData : {
        checkIn:'',
        checkOut:'',
        room_id:localStorage.getItem("room_id")
      }
    };
  },
  mounted() {
    let token=localStorage.getItem("token");
    axios
      .get("http://127.0.0.1:8000/api/access", {
        headers: {
          Authorization: `Bearer ${token}`,
          token: token
        }
      })
      .then(res => {
         this.name=res.data.name  
      });
  },
  methods:{
    RoomBookNow(){
    
      let token=localStorage.getItem("token");

      let endpoint = "http://127.0.0.1:8000/api/book";

      let headers = { 
          Authorization: `Bearer ${token}`,
          token: token
      };

    axios.post(endpoint, this.roomData, {headers})
      .then(response => {
        alert(response.data.message);
      })
      .catch(error => {
        console.log(error.response); // logs an object to the console

      });

    }
  }
};


</script>