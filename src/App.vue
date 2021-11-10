<template>
  <div id="nav">
      <div class="flex  justify-center items-center h-screen ">
        <div class="bg-white px-6  xl:w-1/5 w-5/6 space-y-3 rounded-md">
          <div class="text-2xl font-serif font-bold py-2">Todo App</div>
          <div class="flex ">
            <form @submit.prevent="addTodo">
              <input type="text" v-model="form.title" placeholder="Add your new Todo" class="py-1 px-4 border rounded-md ">
             <button class="px-1 py-1 bg-purple-500 w-8 h-8 text-white font-bold text-2xl mt-1"><p class="-mt-1">+</p></button>
            </form>
            
          </div>
          <div v-if="todos.length">
            <div class="space-y-1 flex" v-for="todo in todos" :key="todo.id">
              <div  @mouseover="mouseOver" @mouseleave="mouseLeave" class="w-full h-8 bg-gray-100 px-1 py-2 text-xs pl-4">{{todo.title}}</div>
            
                  <span v-show="active" @click="deleteTodo" class="bg-red-600 text-white material-icons h-8 w-8 cursor-pointer">delete</span>
                 
            </div>
 
          </div>
            
            <div class="flex py-3 justify-between">
             <div class="text-xs mb-2">You have {{allUndoneTodos}} pending tasks</div>
             <button class="bg-purple-600 px-1 py-3 text-xs text-white -mt-3 w-16 h-8 text-center font-serif" @click="allTodosDone">Clear all
               <div class="-mt-1"></div>
             </button>
            </div>
          
          
         
        </div>
         
      </div>
  
  <router-view/>
  </div>
</template>
<script>
export default{
  data(){
    return{
         form:{
            title:'',
            
         },
         todos:[
           
         ],
         active:false
    }
  },
  methods:{
    addTodo(){
      console.log("clicked");
      this.todos.push({
         title:this.form.title,
         isDone:false
      })
      this.form.title=''
    },
    deleteTodo(todo){
      console.log("Deleted");
      const todoIndex=this.todos.indexOf(todo);
      this.todos.splice(todoIndex);
    },

    mouseOver(){
      this.active =true;   
    },
    mouseLeave(){
      setTimeout(()=>{
this.active=false
      },3000)
      
    },
    allTodosDone(){
      console.log("done");
      this.todos.forEach(todo=>todo.isDone=true)
    }
  },
  computed:{
    
    allUndoneTodos(){
      return this.todos.filter(todo=>!todo.isDone).length
    }
  }
}
</script>
<style>
body{
  background:#7AD7F0;
}
</style>
