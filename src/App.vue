<template>
 <div class="jumbotron bg-primary text-light">
   <div class="container">
    <b>
      <h1 class="dispaly-4">
        Notes
        </h1>
        <p class="lead"> Manage Day to Day task with ease</p>
        </b>
   </div>

 </div>
 <br>
 <br>

 <div class="container">
   <div class="row">
     <div class="col-md-4 offset-4">
       <input type="text" id="taskip" @keydown.enter="insertItem" v-model='todoItem' placeholder="Add note here">
     </div>
   </div>
    <div class="row">
       <div class="col-md-12">
         <h3>Note List</h3>
         <table class="table table-striped">
           <thead class="thead-dark">
             <th>ID</th>
             <th>Name</th>
             <th>Mark as completed</th>
             <th>Remove</th>
           </thead>
           <tbody>
             <tr v-for="(task,index) in todoList" v-bind:key="task">
               <td>{{task.id}}</td>
               <td>
                 <div v-if='!task.editing' @dblclick="editTask(task)" v-bind:class="{completed: task.isCompleted}">{{task.name}}</div>
                 <input @blur="editCompleted(task)" @keydown.enter="editCompleted(task)" v-model="task.name" v-else type="text" name="" id="">
                 </td>
               <td><input v-model="task.isCompleted" type="checkbox"></td>
               <td><button @click="removeItem(index)" class="btn btn-sm btn-danger">Remove</button></td>

             </tr>

           </tbody>
         </table>
       </div>
     </div>
   
 </div>

</template>

<script>

export default {
  data(){
    return{
      todoItem:'',
      id:1,
      todoList:[],
    }
  },
  methods:{
    insertItem(){
      console.log(this.todoItem)
      this.todoList.push({
      name:this.todoItem,
      isCompleted:false,
      id:this.id
      ,editing:false})
      this.id++
      this.todoItem=''
    },
    editTask(task){
      task.editing = true
    },
    editCompleted(task){
      task.editing= false
    },
    removeItem(index){
      this.todoList.splice(index,1)
    }
  }
}
</script>

<style>
#app {

 
}
.completed{
  text-decoration: line-through;
  color: gray;
}

.jumbotron{
  background-color: #651fff  !important;
  box-shadow: 0 40px 20px 0 rgba(0, 0, 0, .2);
}
#taskip{
  border: none;
  border-bottom: 2px solid lightgray;
  width: 300px;
  height: 50px;
  text-align: center;
}
</style>
