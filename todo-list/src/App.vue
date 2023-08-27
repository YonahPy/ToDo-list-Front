<template>
  <div :class="{'template':true, 'dark-theme': isDark, 'light-theme': !isDark}"  id="template">
    <div class="header">
      <h1>TODO</h1>
      <darkMode :isDark="isDark"  @toggleTheme="toggleTheme"/>
    </div>
      <list :class="{'dark-theme': isDark, 'light-theme': !isDark}"/>

    
  </div>
</template>
<script>
  import darkMode from './components/darkMode.vue'
  import list from './components/list.vue'

export default{
  components:{
    darkMode,
    list
  },
  data(){ 
    return{
      isDark: false
  }
    
  },
  methods:{
    toggleTheme(){
      this.isDark = !this.isDark
    }
  }
}

</script>

<style>
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.template{
  background-image: url('../public/images/bg-desktop-light.jpg');
  background-repeat: no-repeat;
  height: 100vh;
  width: 100vw;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding-top: 30px;
  
 
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

.header{
  display: flex;
  width: 70vw;
  justify-content: space-between;
  margin-bottom: 30px;
}
h1{
  display: flex;
  align-self: center;
  font-family: 'Josefin Sans', sans-serif;
  font-size: 40px;
}

</style>
