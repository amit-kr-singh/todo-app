<template>
  <div class="container">
   
   <div class="row no-gutters justify-content-center">
      <h1 class="text-primary font-weight-bold">Todo List</h1>
       <div class="col-lg-12 col-md-12">

        <div class="row no-gutters justify-content-center">
          <div class="col-lg-12 col-md-12">
             <div v-if="!isEditing">
                <input type="text" v-model="todo" style="width:80%;padding: 5px;outline: none;" v-on:keyup.enter="storeTodo">
                <button type="button" class="btn btn-primary" @click="storeTodo">Add</button>
              </div>

              <div v-else>
                <input type="text" v-model="todo" style="width:80%;padding: 5px;outline: none;" v-on:keyup.enter="updateTodo">
                <button type="button" class="btn btn-primary" @click="updateTodo">Update</button>
              </div>
          </div>

          <div class="col-lg-12 col-md-12 mt-4 text-right">
             <ol>
                <li v-for="(todo, index) in todos" :key="index" class="mb-4">
                  <span class="pr-5">{{todo}}</span>
                  <span>
                    <button @click="editTodo(index, todo)" class="btn btn-primary">Edit</button>
                  </span>
                  <span class="pl-5">
                    <button @click="deleteTodo(index)" class="btn btn-danger">Delete</button>
                  </span>
                </li>
             </ol>
          </div>
        </div>
       </div>
   </div>
    
  </div>
</template>

<script>


export default {
  name: 'TodoList',

  data(){
    return {
      isEditing:false,
      selectedIndex:null,
      todo:'',
      todos:["John","Doe"],
    }
  },

  methods: {
    storeTodo(){
      this.todos.push(this.todo)
      this.todo = ''
    },

    editTodo(index, todo){
      this.todo = todo
      this.selectedIndex = index
      this.isEditing = true
    },

    updateTodo(){
      this.todos.splice(this.selectedIndex, 1, this.todo)
      this.todo ='',
      this.isEditing =false;
    },

    deleteTodo(index){
      this.todos.splice(index, 1)
    },

  }
  
}
</script>

<style scoped>
  .container{
    padding: 30px;
    border: 1px solid #f5f5f7;
    box-shadow: 0px 30px 30px 0px rgb(0 11 40 / 10%);
    margin-bottom:40px;
  }
</style>

