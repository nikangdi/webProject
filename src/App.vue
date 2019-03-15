<template>
  <div id="app">
    <input type="text" v-model="todo" @keydown="addData($event)" id="textIn">
    <h2>loading...</h2>
    <ul>
      <li v-for="(item,key) in list" v-if="!item.checked">

        <input type="checkbox" v-model='item.checked' @change="saveDate()">
        {{item.title}}
        <button @click="removeData(key)">删除</button>
      </li>
    </ul>

    <h2>finished</h2>
    <ul>
      <li v-for="(item,key) in list" v-if="item.checked">
        <input type="checkbox" v-model='item.checked' @change="saveDate()" >
        {{item.title}}
        <button @click="removeData(key)">删除</button>
      </li>
    </ul>
    <router-view/>
  </div>
</template>

<script>
import storage from './model/storage.js';
export default {
  name: 'App',
  data(){
    return{
      todo:'',
      list:[],
        }
    },
  methods:{
    removeData(key){
      this.list.splice(key,1),
      storage.set('list',list);
    },
    addData(e){
      if(e.keyCode==13){

        this.list.push({
        title: this.todo,
        checked: false})
      }
      storage.set('list',list);
    },
    saveDate(){
      storage.set('list',this.list)
    },

  },
  mounted(){
    var list = storage.get('list');
    if(list){
      this.list = list;
    }
  }
} 

</script>

<style >
#app{
  text-align: center;
  width: 800px;
   background-color: #ccc;
   margin: 0 auto ; 
   min-height: 700px 
}
#textIn{
  width: 300px;
  height:30px;
  margin-top:30px;
}
#app li{ 
  margin:10px 0;
  transition: all 0.5s;
}
#app li:hover{

  background-color: #ccc;
}
#app ul{
  border: 2px solid black;
  margin: 10px 150px;
  padding: 10px 0;
  background-color:lightblue;
  overflow: hidden;
}

</style>
