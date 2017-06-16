<template>
	<main>
		<chatter-window
			v-for="(chatter, index) in chatters"
		></chatter-window>
		<center-window></center-window>
	</main>
</template>

<script>
	import CONFIG from '../../config.js'

	import ChatterWindow from '../components/ChatterWindow.vue'
	import CenterWindow from '../components/CenterWindow.vue'

    //与服务器建立连接
    socketBus.open('connect', function(){

    })
	export default {
		name: 'chatterroom',
		components: {
			ChatterWindow,
			CenterWindow
		},
		props: [ 'socketBus', 'chatters']
	}
</script>