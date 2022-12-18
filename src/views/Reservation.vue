<template>
<h1>Room Reservation</h1>
Name: <p style="color:#ffffff">{{name}} </p><br>
Email:<p style="color:#ffffff"> {{email}}</p>
</template>


 <script>
import axios from "axios";
export default {
  name: "HelloWorld",
  data() {
    return {
      name: '',
      email: '',
    };
  },
  mounted() {
    let token=localStorage.getItem("token");
    axios
      .get("http://127.0.0.1:8000/api/dashboard", {
        headers: {
          Authorization: `Bearer ${token}`,
          token: token
        }
      })
      .then(res => {
         this.name=res.data.name  
         this.email=res.data.email  
        console.log(res);
      });
  }
};


</script>