<template>

  <div class="hello">

    <div id="posts" v-for="content in blog_content"
    :key="content.id">
      <h1>Post</h1>
      <h2>{{content.userContent}}</h2>
      <p> username: {{content.username}}</p>
      <p>userId: {{content.id}}</p>
    </div>
    <button @click="getblogpost" >Read Previous Post</button>

    <div>

    <input type="text" v-model="username" id="username" placeholder="Enter Username">
    <input type="text" v-model="userContent" id="userContent" placeholder="Enter Post">
    <button @click="blogpost">Post</button>


    <div>
      <input type="text" v-model="userContent" placeholder="Enter Post">
      <input type="text" v-model="userid" placeholder="Enter User ID">
      <button @click="patchblogpost">Update Post</button>
    </div>

    <div>
      <input type="text" v-model="userid" placeholder="Enter User ID">
      <button @click="deleteblogpost">Delete Post</button>
    </div>

  </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'HelloWorld',
  data() {
    return {
      userContent: null,
      username: null,
      userid: null,
      blog_content: []
    }
  },
  methods: {
    blogpost() {
      axios.request({
        url: "http://127.0.0.1:5000/api/blogsite",
        method: "POST",
        data :{
          userContent: this.userContent,
          username: this.username
        }
      }).then((response)=>{
        console.log(response);
        this.getblogpost();
      }).catch((error)=>{
        console.log(error);
      })
      
    },
    getblogpost(){
      axios.request({
        url: "http://127.0.0.1:5000/api/blogsite",
        method:"GET"
      }).then((response)=>{
        console.log(response);
        this.blog_content = response.data;
      }).catch((error)=>{
        console.log(error);
      })
    },
    patchblogpost(){
      axios.request({
        url: "http://127.0.0.1:5000/api/blogsite",
        method:"PATCH",
        data:{
          userContent: this.userContent,
          userid: this.userid
        }
      }).then((response)=>{
        console.log(response);
      }).catch((error)=>{
        console.log(error);
      })
    },
    deleteblogpost(){
      axios.request({
        url:"http://127.0.0.1:5000/api/blogsite",
        method: "DELETE",
        data:{
          userid:this.userid
        }
      }).then((response)=>{
        console.log(response);
      }).catch((error)=>{
        console.log(error);
      })
    }
  },

  mounted () {
    this.getblogpost;
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

#posts{
  
  background-color: lightblue;
  border: 2px black solid;
  h1{
    background-color: cadetblue;
    color: white;
  }
}
input{
  margin: 5px;
  background-color: white;
  padding: 5px 25px;
}
button{
  background-color: rgb(10, 190, 130);
  padding: 5px 10px;
  font-size: 20px;
  color: white;
  margin: 20px;
}
</style>
