<template>
<main>
    <input type="text" v-model="name">
    <button @click="joinRoom">Join</button>
</main>
</template>

<script>
export default {
    name: 'joinWindow',
    props: [ 'socketBus' ],
    data () {
        return {
            name: ''
        }
    },
    methods: {
        joinRoom: function() {
            this.socketBus.emit('chatter joined!', { name: this.name })
        }
    }
}
</script>

<style scoped>
main {
    /*background-color: grey;*/
    position: relative;
    width: 100%;
    height: 100%;
}
</style>