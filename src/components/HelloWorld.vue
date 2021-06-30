<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h3>Helloworld {{youngAge}}</h3>
    <class @onUpdateName="updateParentName" ref ="class"/>
    <h3>Hello word {{name}}</h3>
    <br>
    <button style ="background-color:blue;color:white;font-size:20px" @click="triggerclass">trigger class</button>
    |<br><br>   
  </div>
</template>

<script>
import Class from './Class.vue'
export default {
   name: 'HelloWorld',
   data() {
     return {
       name: ''
       
     }
   },

   computed:{
     youngAge(){
       return this.age - 10;

     }

   },
   watch: {
   age(value) {
     console.log(value);
     this.newAge = value;
   }
   },

   components:{
     Class
   },
   
  props : {
    msg: String,
    age:Number,
  },
  mounted() {
    this.$root.$on("onUpdateName",this.updateParentName);
    this.$on("onUpdateName",this.updateParentName);
  },
  methods: {
  updateParentName(name) {
    this.name = name;
   this.$emit("onUpdateName",name)
  },
  triggerclass(){
    this.$refs.class.onUpdateParent();
    this.name = this.$refs.class.isActive.toString();

  }
  
  }
}
</script>


