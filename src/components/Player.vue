<template>
    <p>{{ player.name }}, <span>{{ showRole(player) }}</span><button v-on:click="$emit('remove-player', player.id)">Entfernen</button></p>
</template>
<script>
export default {
    name: 'Player',
    methods: {
        showRole: function(player){
            if(player.role != 'none') {
                return (', ' + player.role);
            }
            else return '';
        }    
    },
    props: [
        'player'
    ]
}
</script>
<style scoped>

</style>
