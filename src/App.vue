<template>
  <div id="app">
      <h1 v-html="title"></h1>
      <input v-model="newItem" @keyup.enter="addNew"></input>

      <ul>
        <li v-for="item in items" v-bind:class="{finished:item.isFinished}" v-on:click="finish(item)">
          {{item.label}}
        </li>
      </ul>

      <p v-if="childWords!=''">children tell me:{{childWords}}</p>
      <component-a msgfromfather='Msg from App.vue in the componentA!' v-on:childtellme='listen'></component-a>
      <!-- 必须转成小写,componentA=>component-a -->
  </div>



</template>

<script>
import Store from './store'
import componentA from './components/componentA'

export default {
  data:function(){
    return{
      title:'<a>This is a todo list</a>',
      items:Store.fetch()||[],
      newItem:'',
      childWords:''
    }
  },
  components:{componentA},
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
    },
    listen:function(msg){
      this.childWords=msg;
    },

  },
  watch:{
    items:{
      handler:function(items){
        Store.save(items);
      }
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

ul{
  margin-left: 130px;
  position:absolute;
}

p{
  margin-top: 200px;
}

</style>
