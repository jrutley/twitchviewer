<template>
  <div id="app">
    <h1>Twitch Viewer</h1>

    <table class="table table-hover table-bordered">
        <thead>
            <tr>
            <td>Logo</td>
            <td>Streamer</td>
            <td>Status</td>
            </tr>
        </thead>
        <tbody>
        <tr v-for="s in streamers" v-bind:data-href="s.url">
            <td>{{s.icon}}</td>
            <td>{{s.user}}</td>
            <td>{{s.status}}</td>
        </tr>
        </tbody>
    </table>
</div>
</template>

<script>
    // API call to Twitch.
    const baseUri = "https://wind-bow.gomix.me/twitch-api/";
    let stream = "streams/";
    let fcc = "freecodecamp";
    let test = "test_channel";

    let streams = [{
        icon: "myicon",
        user: fcc,
        status: baseUri + test
    }];

    // foreach streamer

    // On response, fill up a property on the data section

    export default {
        name: 'app',
        data() {
            return {
                streams: [fcc, test, "ESL_SC2"],
                streamers: [],
            };
        },
        methods: {
            liveStream: function() {
                return this.streams.map(s => {
                    return this.$http.get(baseUri + stream + s).then(r => {
                        let response = r.body;
                        if (response.stream === null) {
                            return {
                                icon: "myicon",
                                user: s,
                                status: "Offline",
                                // TODO: Call this link in order to get the channel and get url prop from there
                                url: response._links.channel
                            };
                        } else {
                            return {
                                icon: "myicon",
                                user: s,
                                status: response.stream.game,
                                url: response._links.channel
                            };
                        }
                    }).catch(console.log.bind(console));
                }, response => {
                    // error callback
                    console.log(response);
                    return response;
                });
            }

        },
        mounted: function() {
            this.liveStream().map(streamPromise => {
                streamPromise.then(s => {
                    this.streamers.push(s);
                });
            });
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
</style>