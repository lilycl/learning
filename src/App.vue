<template>
  <div id="app">

    <h1 v-text="title"></h1>
     <input v-model="newItem" v-on:keyup.enter="addNew">
    <ul>
        <li v-for="item in items" v-bind:class="{finished: item.isFinished}" v-on:click="toggleFinish(item)">{{item.label}}</li>
    </ul>
    <p>aaaddd: {{childwords}}</p>
    <comA sendmsg='to child' v-on:send-by-child='toParents'></comA>
  </div>
</template>

<script>
import store from "./store"
import comA from "./components/comA"

export default {
 data:function(){
    return{
    title:'this is a todo list',
    items:store.fetch(),
    newItem:'',
    childwords:''
    }
 },
 components:{comA},
 watch:{
  items:{
   handler:function(val,oldVal){
       console.log(val,oldVal)
   },
   deep:true
  }
 },
 events:{
    'send-by-child':function(msg){
       this.childwords = msg
    }
 },
 methods:{
  toggleFinish: function(item){
    item.isFinished = !item.isFinished
  },
  addNew: function(){
    this.items.push({
       label:this.newItem,
       isFinished:false
    }),
    this.newItem =''
    this.$broadcast('onAddnew',this.items)
  },
  toParents:function(msg){
      this.childwords = msg;
  }
 }
}
</script>

<style>
.finished{text-decoration:underline;}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
