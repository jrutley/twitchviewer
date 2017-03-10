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
            <td><a :href="s.url"><img class="img-circle" width="50px" :src="s.icon"></a></td>
            <td><a :href="s.url">{{s.user}}</a></td>
            <td><a :href="s.url">{{s.status}}</a></td>
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
                streams: [fcc, test, "ESL_SC2", "OgamingSC2", "cretetion", "freecodecamp", "storbeck", "habathcx", "RobotCaleb", "noobs2ninjas"],
                streamers: [],
            };
        },
        methods: {
            liveStream: function() {
                return this.streams.map(s => {
                    return this.$http.get(baseUri + stream + s).then(r => {
                        let response = r.body;
                        let channel = baseUri + "channels/" + response._links.channel.split('/').splice(-1)[0]
                        return {
                            user: s,
                            status: response.stream,
                            url: this.$http.get(channel).then(u => {
                                return u.body;
                            }).catch(console.log.bind(console))
                        };
                    }).catch(console.log.bind(console));
                }, response => {
                    console.log(response);
                    return response;
                });
            }

        },
        mounted: function() {
            this.liveStream().map(streamPromise => {
                streamPromise.then(s => {
                    s.url.then(u => {
                        let x = {
                            icon: (u.logo === undefined || u.logo === null) ? "https://rlv.zcache.com/big_goose_egg_games_postcard-reaf3f877bf9e41249bde4f4b03bb130c_vgbaq_8byvr_324.jpg" : u.logo,
                            user: s.user,
                            status: s.status === null ? "Offline" : s.status.game + " " + u.status,
                            url: u.url
                        }
                        this.streamers.push(x);
                    }).catch(console.log.bind(console));
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
    
    td a {
        display: block;
    }
</style>