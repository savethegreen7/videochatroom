<template>
    <div>
        <chatter-room :socket-bus="socket" :chatters="chatters"></chatter-room>
    </div>
</template>

<script>
    import io from 'socket.io-client'

    import chatterRoom from './views/chatterRoom.vue'
    import joinWindow from './views/joinWindow.vue'

    import webRTC from './common/webRTC.js'
    import CONFIG from '../config.js'

    //开启socket端口2018
    var socket = io.connect(`https://${CONFIG.DEV_IP}:${CONFIG.SOCKET_PORT}`)

    export default {
        name: 'app',
        components: {
            chatterRoom,
            joinWindow
        },
        data () {
            return {
                socket: socket,
                chatters: []
            }
        },
        created () {
            this.socket.on('chatter join success', data => {
              this.chatters.push(data);
            })
        }
    }
</script>