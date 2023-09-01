<template>
    <main>
        <div class="input">
            <input type="text"  v-if="!showCompletedTasks" placeholder="Create a new todo..." id="text" v-model="newTask" @keyup.enter="addTask">
        </div>
        <div class="all">
            <ul class="all-tasks" v-if="!showCompletedTasks && !showActiveTasks  || showAllTasks">
                <Tasks v-for="(task, index) in tasks" :key="index"  :tasks="task" @deleteTasks="deleteTask(index)" @currentTask="currentTask" ></Tasks>

            </ul>
            <listCompleted :listCompleted="completedTasks"  v-if="showCompletedTasks">

            </listCompleted>

            <listActive :listActive="activeTasks" v-if="showActiveTasks">

            </listActive>
            
            <ul class="filter">
            <li class="filter-item"> 5 items left</li>
            <li class="filter-item" @click="showFilterAllTasks">All</li>
            <li class="filter-item" @click="showFilterActiveTasks">Active</li>
            <li class="filter-item" @click="showFilterCompletedTasks">Completed</li>
            <li class="filter-item">Clear completed</li>
            </ul>
        </div>


    </main>
</template>

<script>
import Tasks from './tasks.vue'
import listCompleted from './completedTasks.vue'
import listActive from './activeTasks.vue'

export default{
    components:{
        Tasks,
        listCompleted,
        listActive
    },
    data(){
        return{
            newTask: '',
            tasks: [],
            activeTasks: [],
            completedTasks: [],
            showCompletedTasks: false,
            showActiveTasks: false,
            showAllTasks: true

        };
    },
    watch:{
        showCompletedTasks(newVal) {
            if (newVal) {
            this.showActiveTasks = false;
            this.showAllTasks = false;
            }
        },
        showActiveTasks(newVal) {
            if (newVal) {
            this.showCompletedTasks = false;
            this.showAllTasks = false;
            }
        },
        showAllTasks(newVal) {
            if (newVal) {
            this.showCompletedTasks = false;
            this.showActiveTasks = false;
            }}
        
        
        },
    methods:{
        addTask(){
            if (this.newTask.trim() !== ''){
                this.tasks.push(this.newTask);
                this.activeTasks.push(this.newTask)
                this.newTask = '';
            }
        },
        deleteTask(index){
            this.tasks.splice(index, 1);
            this.activeTasks.splice(index, 1);
            this.removeCompletedTasksNotInTasks();
        },
        currentTask(isChecked, taskName){
            if (isChecked){
                this.completedTasks.push(taskName)
                const indexinActiveTasks = this.activeTasks.indexOf(taskName)
                if(indexinActiveTasks !== -1){
                    this.activeTasks.splice(indexinActiveTasks,1)
                }
            } else{
                this.activeTasks.push(taskName);
                const indexInCompletedTasks = this.completedTasks.indexOf(taskName)
                if(indexInCompletedTasks !== -1){
                    this.completedTasks.splice(indexInCompletedTasks, 1)
                }
            }
        },
        removeCompletedTasksNotInTasks() {
            if (this.completedTasks.length > 0) {
            this.completedTasks.forEach((tasksComp, index) => {
                if (!this.tasks.includes(tasksComp)) {
                this.completedTasks.splice(index, 1);
                }
            });
            }
        },
        showFilterCompletedTasks(){
            this.showCompletedTasks = !this.showCompletedTasks
 
        },
        showFilterActiveTasks(){
            this.showActiveTasks = !this.showActiveTasks
           
        },
        showFilterAllTasks(){
            this.showAllTasks = !this.showAllTasks
        }
    }
}

</script>

<style scoped>
main{
    background-color:transparent;
    color: black;
    border-radius: 10px;
    padding: 15px;
    box-shadow: 3px 3px 10px black;
}
.all{
    
    margin-top: 10px;
    border-radius: 15px;
    padding: 5px;
}
.input{
    padding: 5px;
    border-radius: 10px;
    
    
}

input{
    border: none;
    width: 70vw;
    padding: 20px;

}
.dark-theme{
  background-color: hsl(235, 21%, 11%);
  color: white;
  transition: background-color 0.5s ease 0.1s;
  
}
.light-theme{
  transition: background-color 0.5s ease 0.1s;
  background-color: rgb(255, 255, 255);
  color: rgb(0, 0, 0);
}
input:focus{
    outline: none;
    
}
.all-tasks{
    padding: 5px;
}
.filter{
    display: flex;
    padding: 15px;
    justify-content: space-evenly;
}
.filter-item{
    list-style: none;
    font-size: 13px;
}
.filter-item:hover{
    color: hsl(220, 98%, 61%);
    cursor: pointer;
}
</style>