<template>
    <div id="app" class="row div-grid">
        <div id="nav">
        <!-- <router-link to="/">Home</router-link> | -->
        <!-- <router-link to="/about">About</router-link> | -->
        <!-- <router-link to="/schedule">Criar Escala</router-link> -->
        </div>
        <!-- <router-view/> -->
        <!-- Exibe o clendario -->
        <schedule />
        <formFunctionary />
    </div>
</template>
<script>
import Schedule from './components/Schedule.vue';
import FormFunctionary from './components/FormFunctionary.vue';

export default {
    components: {
        Schedule,
        FormFunctionary
    },
    methods: {
 
    }
}
</script>

<style lang="scss">
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
}

#nav {
    padding: 30px;

    a {
        font-weight: bold;
        color: #2c3e50;

        &.router-link-exact-active {
        color: #42b983;
        }
    }
}
</style>
