<template>
  <div id="app">
    <h1>Twitch Viewer</h1>

    <div class="container">
        <table class="table table-hover">
            <tr>
                <td>ICON</td>
                <td>My user</td>
                <td>What am I streaming at the moment?</td>
            </tr>
            <tr class="active">
                <td>ICON</td>
                <td>My user</td>
                <td>What am I streaming at the moment?</td>
            </tr>
        </table>
    </div>
  </div>
</template>

<script>
    export default {
        name: 'app',
        data() {
            return {
                msg: 'Welcome to Your Vue.js App'
            }
        }
    }
</script>

<style lang="scss">
    #app {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
        border: 1px solid black;
    }
    
    h1,
    h2 {
        font-weight: normal;
    }
    
    ul {
        list-style-type: none;
        padding: 0;
    }
    
    li {
        display: inline-block;
        margin: 0 10px;
    }
    
    a {
        color: #42b983;
    }
    /*.active {
        background-color: #42b983;
    }*/
</style>