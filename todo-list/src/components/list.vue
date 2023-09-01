<template>
    <main>
        <div class="input">
            <input type="text" placeholder="Create a new todo..." id="text" v-model="newTask" @keyup.enter="addTask">
        </div>
        <div class="all">
            <ul class="all-tasks">
                <Tasks v-for="(task, index) in tasks" :key="index"  :tasks="task" @deleteTasks="deleteTask(index)" @currentTask="currentTask"  ></Tasks>

            </ul>
            <listCompleted :listCompleted="completedTasks"  v-if="showCompletedTasks">

            </listCompleted>
            
            <ul class="filter">
            <li class="filter-item"> 5 items left</li>
            <li class="filter-item">All {{ tasks }}</li>
            <li class="filter-item">Active {{ activeTasks }}</li>
            <li class="filter-item" @click="showFilterCompletedTasks">Completed</li>
            <li class="filter-item">Clear Completed</li>
            </ul>
        </div>


    </main>
</template>

<script>
import Tasks from './tasks.vue'
import listCompleted from './completedTasks.vue'

export default{
    components:{
        Tasks,
        listCompleted
    },
    data(){
        return{
            newTask: '',
            tasks: [],
            activeTasks: [],
            completedTasks: [],
            showCompletedTasks: false
            

        };
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
        }
    }
}

</script>

<style scoped>
main{
    background-color:transparent;
    color: black;
}
.all{
    background: white;
    margin-top: 10px;
    border-radius: 15px;
    padding: 5px;
}
.input{
    padding: 5px;
    border-radius: 10px;
    background: white;
    
}
input{
    border: none;
    width: 70vw;
    padding: 20px;

}
input:focus{
    outline: none;
    
}
.all-tasks{
    
    padding: 5px;
    background-color:white ;
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
</style>