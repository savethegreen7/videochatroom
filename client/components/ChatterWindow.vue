<template>
	<div class="player" :style="layout">
		<video v-show="chatter.isJoined" :src="chatter.src" autoplay></video>
		<button v-if="!chatter.isJoined" class="join" @click="join">+</button>
		<span class="name">{{ chatter.name }}</span>
		<span class="close"></span>
	</div>
</template>

<script>
    var getUserMedia = (navigator.getUserMedia || navigator.webkitGetUserMedia ||navigator.mozGetUserMedia || navigator.msGetUserMedia);
    var PeerConnection = (window.PeerConnection || window.webkitPeerConnection00 ||window.webkitRTCPeerConnection || window.mozRTCPeerConnection);
	var URL = (window.URL || window.webkitURL || window.msURL || window.oURL);
	var nativeRTCIceCandidate = (window.mozRTCIceCandidate || window.RTCIceCandidate);
    var nativeRTCSessionDescription = (window.mozRTCSessionDescription || windowRTCSessionDescription); 
    var moz = !!navigator.mozGetUserMedia;
    var packetSize = 1000;

    //发送ICE候选到其他客户端
    pc.onicecandidate = function(event){
    	socketBus.send(JSON.stringify({
    		socket.sned(JSON.stringify({
    			"event": "__ice_candidate",
    			"data": {
    				"candidate": event.candidate
    			}
    		}))
    	}))
    }
	export default {
		name: 'ChatterWindow',
		props: [ 'chatter', 'layout', 'socketBus' ],
		data () {
			return {
				chatterMediaSource: {},
				videoStream: [],
				initializedStreams: 0,
				peerConnections: 0
			}
		},
		methods: {
			//聊天者加入房间
			chatStream: function () {
				let constraints = { audio: true, video: { width: 400, height: 300 } };
				if (getUserMedia) {
					getUserMedia.call(navigator,constraints,function (stream) {
						this.videoStream = stream;
						socketBus.emit("we are chatting", stream);
					},
					function(error) {
						socketBus.emit("failed", error);
					})
				} else {
					socketBus.emit("WebRTC is not yet supported in this browser~");
				}
			}
		}

	}
</script>