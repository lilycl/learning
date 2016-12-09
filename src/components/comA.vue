<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h1>{{ sendmsg }}</h1>
    <button v-on:click="onClickMe">click!</button>
  </div>
</template>

<script>
export default {
  name: 'hello',
  data: function() {
    return {
      msg: 'in component'
    }
  },
  props:['sendmsg'],
  events:{
    'onAddnew': function(items){
        console.log(items)
    }
  },
  methods:{
    onClickMe:function(){
      console.log(this.sendmsg)
      this.$dispatch('send-by-child', this.msg);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
