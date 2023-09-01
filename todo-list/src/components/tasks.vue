<template>
    <div class="tasks">

        <div class="set">
            <button @click="checkTask" :class="{'check':true , 'checked': isChecked}">
            <img src="../../public/images/icon-check.svg" alt="check" id="image-checked">
            </button>
            <li :class="{'li-checked':isChecked}">{{ tasks }}</li>
            <button id="delete" @click="$emit('deleteTasks', index)">
                <img src="../../public/images/icon-cross.svg" alt="delete">
            </button> <br>
        </div>
  
        <div class="line"></div>

        
    </div>
</template>

<script>
export default{
    data(){
        return{
            isChecked: false,
            

        }
    },
    props:{
        tasks:String,

    },
    methods:{
        checkTask(){
            this.isChecked = !this.isChecked;
            const img = document.getElementById('image-checked');
            this.$emit('currentTask', this.isChecked, this.tasks)
            if (this.isChecked){
                img.style.display = 'inline'
            }else{
                img.style.display = 'none'
            }
        },
  
    
}}
</script>

<style scoped>
:root {
  --check-gradient: linear-gradient(to bottom right, hsl(192, 100%, 67%), hsl(280, 87%, 65%));
}
.tasks{
    display: flex;
    flex-direction: column;
    width: 70vw;
    
    
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

.set{
    display: flex;
    padding: 7px 0px 7px 0px;
}
.line{
    height: 1px;
    background-color:hsl(236, 9%, 61%);
    margin-block: 10px;

}
li{
    list-style: none;
    font-size: 21px;
    font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
}
.li-checked{
    text-decoration: line-through;
    color: rgba(54, 43, 43, 0.541);
}

.check{
    border-radius: 50%;
    border: 1px solid hsl(192, 100%, 67%);
    width: 23px;
    height: 23px;
    margin-inline: 15px;

}
.check img{
    display: none;
}
.checked{
    background: linear-gradient(to bottom right, hsl(192, 100%, 67%), hsl(280, 87%, 65%));
}
.checked img{
    display: inline;
}



#delete{
    width: 23px;
    height: 23px;
    border: none;
    font-size: 25px;
    background-color: transparent;
    opacity: 0;
    transition: opacity 0.2s ease, visibility 0.3s ease;
    margin-left: auto;
    margin-right: 15px;
}
.tasks:hover #delete{
    visibility: visible; 
    opacity: 1;
}

</style>

