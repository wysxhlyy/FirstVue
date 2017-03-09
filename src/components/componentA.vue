<template>
  <div class="hello">
    <h1>{{msg}}</h1>
    <h2>{{msgfromfather}}</h2>
    <button v-on:click="onClickMe">Get Msg from componentA</button>

  </div>

</template>

<script>
export default {
  data () {
    return {
      msg: 'Hello from component A'
    }
  },
  props:['msgfromfather'],
  // 父组件往子组件传参
  methods:{
    dothis: function(){
      alert("hello");
    },
    onClickMe:function(){
      //console.log(this.msgfromfather);
      this.$emit("childtellme",this.msg);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1{
  margin-top: 200px;
}
</style>
