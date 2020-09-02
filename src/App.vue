<template>
  <div id="app">
    <Mylist v-bind:title="message"
    v-on:result-event="appAction" />
  </div>
</template>

<script>
import Mylist from './components/Mylist.vue'

export default {
  name: 'App',
  components: {
    Mylist
  },
  data: function(){
    return {
      message:'メモを入力してください',
      result:[],
    };
  },
  computed:{
    log:function(){
      var table = '<tr><th class="head">Mylist</th></tr>;
      for(var i in this.result){
        table += '<tr><td>' + this.result[i] + '</td>';
      }
      return table;
    }
  },
  created: function(){
    var items = localStorage.getItem('log');
    var logs = JSON.parse(items);
    if (logs != null){ this.result = logs;}
  },
  methods:{
    appAction: function(exp,res) {
      this.result.unshift([exp,res]);
      if(this.result.length > 5){
        this.result.pop();
      }
      var log = JSON.stringify(this.result);
      localStorage.setItem('log',log);
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
tr td {
  padding:5px;
  border:lpx solid gray;
}
tr th {
  padding:5px;
  border:lpx solid gray;
}
tr th.head {
  background-color: black;
  color:white;
}
</style>
