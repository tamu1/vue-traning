<template>
  <div id="app">
    
    <h1>{{newName}}</h1>
    <img alt="Vue logo" src="./assets/logo.png" />
    <div></div>
    
    <!-- <input type="text" v-model="message"> -->
    <HelloWorld msg="tamana" :age="num" @onUpdateName="updateName"/>
    <!--<class v-bind:name="num" @onUpdateName="updateName" />-->
    <!--<div v-if="num == 4">Paras</div>
    <div v-else-if="num == 55">Prince</div>
    <div v-else>Tamanna</div>
    <div v-for="index in names" v-bind:key="index.id">
      {{ index.id }} {{ index.name }}
    </div>
    <button v-on:click="clicked">click here</button>
    <button @click="clicked">click here</button>
    <h1>{{ newData }}</h1>
    <input type="text" v-model="newData">-->

    
    <button @click="getDummyData">Get posts</button> <br><br>
    <input @change="SayHello('changeEvent')" v-model="num" type="text">
    <div class="List">
      <ul class="List-ul">
        <li v-for="post in posts" :key="post.id">{{post.title}}</li>
        </ul>
        </div>

        
  
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
//import Class from "./components/Class.vue";
import axios from 'axios';

export default {
  name: "App",
  components: {
    HelloWorld,
   // Class
    
   },
  created() {
    this.sayHello("created hello");
    this.num = 55;
  },
  mounted() {
   // this.sayHello("mounted hello");
    this.num = 20;
    this.$root.$on("onUpdateName",this.updateName);
  },
  data() {
    return {
      num: 4,
      names: [
        {
          id: 1,
          name: "paras",
        },
        {
          id: 2,
          name: "tamanna",
        },
        {
          id: 3,
          name: "prince",
        },
      ],
      newData : "Data to be update",
      posts:[],
      newName:"prince"


    };
  },

  methods: {
    sayHello(greetings) {
      console.log(greetings);
      return greetings;
    },
    clicked() {
      this.newData = "clicked";
    },
    async getDummyData(){
      axios.get('https://jsonplaceholder.typicode.com/posts')
      .then(response => {
        this.posts = response.data;
      
      })
    

      .catch((error) => {
        console.log(error.response.data);
      })
   },
   updateName(event){
     this.newName = event;
     //this.$emit("");

   }
}
}
    
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
