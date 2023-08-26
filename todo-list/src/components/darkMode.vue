<template>
        <button @click="toggleMode, $emit('toggleTheme')">
            <img :src="imagePath" alt="dfs" id="imagem">
        </button>

    
</template>
<script>


export default{
    props:{
        isDark: Boolean
    },
    computed:{
        imagePath() {
        return this.isDark ? '../../public/images/icon-sun.svg' : '../../public/images/icon-moon.svg';
    }
}
}

</script>
<style scoped>
button{
    width: 80px;
    height: 70px;
    border: none;
    cursor: pointer;
    background-color: transparent;
}
</style>