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
    let streamUri = "streams/";
    let fcc = "freecodecamp";
    let test = "test_channel";

    let streams = [{
        icon: "myicon",
        user: fcc,
        status: baseUri + test
    }];

    function* getLiveStream(that, currentStream) {
        const r = yield that.$http.get(baseUri + streamUri + currentStream);
        const response = r.body;
        const channel = baseUri + "channels/" + response._links.channel.split('/').splice(-1)[0];
        const myUrl = yield that.$http.get(channel);
        return {
            user: currentStream,
            status: response.stream,
            url: myUrl.body
        };
    }

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
                    let sg = getLiveStream(this, s);
                    return sg.next().value // should be r
                        .then(r => sg.next(r).value)
                        .then(myUrl => sg.next(myUrl).value)
                        .catch(console.log.bind(console));
                }, response => {
                    console.log(response);
                    return response;
                });
            }

        },
        mounted: function() {
            this.liveStream().map(streamPromise => {
                streamPromise.then(s => {
                    const u = s.url;
                    let x = {
                        icon: (u.logo === undefined || u.logo === null) ? "http://res.cloudinary.com/jrutley/image/upload/v1489329014/big_goose_egg.jpg" : u.logo,
                        user: s.user,
                        status: s.status === null ? "Offline" : s.status.game + " " + u.status,
                        url: u.url
                    }
                    this.streamers.push(x);
                }).catch(console.log.bind(console));
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