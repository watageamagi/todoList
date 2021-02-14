<template>
    <div id="app">
        <input v-model="todoObj.text"/>
        <button type="submit" @click="Howtodo" >送信</button>

        <b-list-group>
          <b-list-group-item v-for="(obj ,index) in todoList" :key="index+1">
            <b-form-checkbox
              v-model="obj.check"
            >
          </b-form-checkbox> {{ obj.text }}  
            <button @click="deleteTodo(index)">削除</button>
            <button @click="exchange(obj)">編集</button>
            <input v-if="obj.edit == true" v-model="obj.text"  />
            </b-list-group-item>
        </b-list-group>
    </div>

    
</template>

<script>
export default {
  data(){
    return{
      message : '',
      todoList :[],
      todoObj: new Object({
        text: '',
        check:false,
        edit:false,
      })
    }
  },
  mounted(){
    if(localStorage.getItem('todoList')){
      try{
        this.todoList = JSON.parse(localStorage.getItem('todoList'));
      }catch(e) {
        localStorage.removeItem('todoList');
      } 
    }
  },


  methods: {
      Howtodo(){
        if(!this.todoObj.text){
          return
        }

        this.todoList.push(this.todoObj)  //todoListにtodoObjをブチ込む
        this.todoObj = new Object({
        text: '',
        check:false,
        })
        this.saveTodo();
      },

      deleteTodo(index){
        this.todoList.splice(index,1)
        this.saveTodo();
      },

      exchange(obj){
        obj.edit = !obj.edit //オブジェクトeditのfalseをtureに
        this.saveTodo();
      },

      saveTodo(){
        const parsed = JSON.stringify(this.todoList);
        localStorage.setItem('todoList', parsed);
        console.log(localStorage)
      }

  }

}
</script>


<style lang="scss" scoped>

</style>