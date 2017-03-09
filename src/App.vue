<template>
  <div id="app">
      <h1 v-html="title"></h1>
      <input v-model="newItem" @keyup.enter="addNew"></input>

      <ul>
        <li v-for="item in items" v-bind:class="{finished:item.isFinished}" v-on:click="finish(item)">
          {{item.label}}
        </li>
      </ul>
  </div>



</template>

<script>
export default {
  data:function(){
    return{
      title:'<a>This is a todo list</a>',
      items:[
        {
          label: 'coding',
          isFinished:false
        },
        {
          label:'walking',
          isFinished:false
        }
      ],
      newItem:''
    }
  },
  methods:{
    finish:function(item){
      item.isFinished=!item.isFinished;
    },
    addNew:function(){
      this.items.push({
        label:this.newItem,
        isFinished:false
      })
      this.newItem='';
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.finished{
  text-decoration: underline;
}
</style>
