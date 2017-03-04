<template>
  <div id="app">
    <h1>Twitch Viewer</h1>

    <table class="table table-hover table-bordered">
        <thead>
            <tr>
            <td>MOn icon</td>
            <td>Le user</td>
            <td>Les details</td>
            </tr>
        </thead>
        <tbody>
        <tr>
            <td class="active">ICON</td>
            <td class="danger">My user</td>
            <td>What am I streaming at the moment?</td>
        </tr>
        <tr class="active">
            <td>ICON</td>
            <td>My user</td>
            <td>What am I streaming at the moment?</td>
        </tr>
        <tr class="active">
            <td>ICON</td>
            <td>My user</td>
            <td>What am I streaming at the moment?</td>
        </tr>
        </tbody>
    </table>
    <div>
        <span class="label label-info">Testing 1-2-3</span>
        <span class="label label-danger">Danger will robinson</span>
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
    @import "../node_modules/bootstrap/dist/css/bootstrap.min.css";
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