<template>
<div class = "container ">
  <h2 class="text-center mt-5">Todo App</h2>

  <div class="d-flex">
    <input v-model="task" type="text" placeholder = "Enter task" class="form-control">
    <button @click="submitTask" class="btn button-warning rounded-0">SUBMIT</button>
  </div>

  <table class="table table-bordered">
  <thead>
    <tr>
      <th scope="col">Task</th>
      <th scope="col">Status</th>
      <th scope="col" class = "text-center">#</th>
      <th scope="col" class = "text-center">#</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(task , index) in tasks" :key="index">
      <td>{{task.name}}</td>
      <td style="width: 120px"><span @click = "changeStatus(index)" class = "pointer">{{task.status}}</span></td>
      <td>
        <div class = "text-center" @click="editTask(index)">
          <span class="fa fa-pen"></span>
        </div>
        </td>
      <td>
        <div class = "text-center" @click="deleteTask(index)">
          <span class = "fa fa-trash"></span>
        </div>
      </td>
    </tr>
  </tbody>
</table>
  </div>
</template>

<script>
export default {
  mounted() {
      this.tasks = JSON.parse(localStorage.getItem('tasks'))
    },
  name: 'HelloWorld',
  data() {
    return {
      task: "Hello world",
      editedTask: null,
      availableStatus: ["to-do","in-progress", "finished"],
      tasks: [
        {
          name: "steal bananas",
          status: "to-do"
        },
         {
          name: "eat bananas",
          status: "to-do"
        }
      ]
    }
  },
  watch: {
   tasks: function () {
     this.saveData()
   }
  },

  methods: {
    submitTask(){
      if(this.task.length === 0) return;

      if(this.editedTask === null) {
        this.tasks.push({
          name: this.task,
          status: "to-do"
        })
      } else {
        this.tasks[this.editedTask].name = this.task;
        this.tasks.
        this.editedTask = null;
      }
      
      this.task = " ";
    },

    deleteTask(index){
      this.tasks.splice(index, 1);
    },

    editTask(index){
      this.task = this.tasks[index].name;
      this.editedTask = index;
    },

    changeStatus(index) {
        let newindex = this.availableStatus.indexOf(this.tasks[index].status)
        if(++newindex > 2) newindex = 0
        this.tasks[index].status = this.availableStatus[newindex]
    },

    saveData(){
      const stringTasks = JSON.stringify(this.tasks)
      localStorage.setItem('tasks', stringTasks)
    }
  }
}
</script>

<style scoped>
.pointer {
  cursor: pointer;
}
</style>

