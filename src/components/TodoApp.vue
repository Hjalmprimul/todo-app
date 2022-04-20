<template>
  <div class="conteiner">
    <h2 class="text-center mt-5">My Vue Todo App</h2>

    <!-- Input -->
    <div class="d-flex">
      <input v-model="task" type="text" placeholder="Enter Task" class="form-control" />
      <button @click="submitTask" class="btn btn-warning rounded-0">SUBMIT</button>
    </div>

    <!-- Task table -->
    <table class="table table-bordered mt-5">
      <thead>
        <tr>
          <th scope="col" class="text-center">Task </th>
          <th scope="col" class="text-center">Status</th>
          <th scope="col" class="text-center">#</th>
          <th scope="col" class="text-center">#</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, index) in tasks" :key="index">
          <th :class="{'finished': task.status == 'finished'}">{{firstCharUpper(task.name)}}</th>
          <td @click="changeStatus(index)" class="pointer" style="width: 120px"
          :class="{'text-danger': task.status === 'to-do',
                   'text-warning': task.status === 'in-progress',
                   'text-success': task.status === 'finished'}">
            {{firstCharUpper(task.status)}}
          </td>
          <td @click="editTask(index)" class="text-center pointer">
              <font-awesome-icon icon="fa-solid fa-pen"/>
          </td>
          <td @click="deleteTask(index)" class="text-center pointer">
              <font-awesome-icon icon="fa-solid fa-trash"/>
          </td>
        </tr>
        
      </tbody>
    </table>
  </div>
</template>

<script>
    export default {
        name: 'conteiner',
        data(){
            return{
                task: '',
                editedTask: null,
                availeableStatus: ['to-do','in-progress','finished'],

                tasks:[
                    {
                        name: 'comprar pan',
                        status: 'to-do'
                    },
                    {
                        name: 'pasear al perro',
                        status: 'in-progress'
                    }
                ]
            }
        },
        methods:{
            submitTask(){
                if(this.task.length === 0) return;

                if(this.editedTask === null){
                    this.tasks.push({
                        name: this.task,
                        status: 'to-do'
                    })
                } else{
                    this.tasks[this.editedTask].name = this.task;
                    this.editedTask = null;
                }

                this.task = '';
            },
            deleteTask(index){
                this.tasks.splice(index, 1);
            },
            editTask(index){
                this.task = this.tasks[index].name
                this.editedTask = index
            },
            changeStatus(index){
                let newIndex = this.availeableStatus.indexOf(this.tasks[index].status);
                if(++newIndex > 2) newIndex = 0;
                this.tasks[index].status = this.availeableStatus[newIndex];
            },
            firstCharUpper(string){
                return string.charAt(0).toUpperCase() + string.slice(1);
            }
        }
    };
</script>

<style>
.conteiner{
    display: block;
    margin-left: 10%;
}
.pointer{
    cursor: pointer;
}
.finished{
    text-decoration: line-through;
}
</style>