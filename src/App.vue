<template>
  <div id="app">
    <Mylist v-bind:msg="title" v-on:result-event="appAct" />
    <hr>
    <table v-html="list" align='center' border='1'></table>
  </div>
</template>

<script>
import Mylist from './components/Mylist.vue'

export default {
  name: 'App',
  components: {
    Mylist
  },
  data:function(){
    return {
      title:'メモを入力してください',
      memo:[],
    }
  },
  computed:{
    list:function(){
      var table = '<tr><th class="head">my list</tr></tr>';
      for(var i in this.memo){
        table += '<tr><td>' + this.memo[i] + '</td></tr>';
      }
      return table;
    }
  },
  created:function(){
    var items = localStorage.getItem('list');
    var lists = JSON.parse(items);
    if(lists != null){ this.result = lists; }
  },
  methods:{
    appAct:function(input){
      this.memo.unshift(input);
      if(this.memo.length > 5){
        this.memo.pop();
      }
      var list = JSON.stringify(this.result);
      localStorage.setItem('list',list);
    },
  },
  
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
