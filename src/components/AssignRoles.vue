<template>
    <div>
        <button v-on:click="fillRoleQueue">Rollen-Queue füllen</button>
        <button v-on:click="makeRoles">Rollen verteilen</button>
    </div>
</template>

<script>
export default {
    name: 'AssignRoles',
    data() {
        return {
                rolesQueue: []
            }
    },
    methods: {
        makeRoles(e) {
            e.preventDefault();
            var roleQueue = this.fillRoleQueue();
            var player;
            if (roleQueue.length !=  this.players.length) {
                    alert('Rollen und Spieler sind nicht identisch')
                    return 0;
                }
            for(player in this.players){
                var rd = Math.floor(Math.random() * roleQueue.length);
                this.players[player].role = roleQueue[rd];
                roleQueue = roleQueue.splice(rd, 1);
                }
            },
        fillRoleQueue() {
            var roleQueue = [];
            var role;
            for (role in this.roles) {
                var toAdd = this.roles[role].name;
                //alert('Ich nehme jetzt ' + toAdd + " her!");
                for (var i = this.roles[role].qty; i>0; i--) {
                    roleQueue.push(toAdd);
                    }
                }
            this.rolesQueue = roleQueue;
            return roleQueue;
            },
            
        },
    props: [
        'players',
        'roles'
        ]
        
}
</script>

<style scoped>

</style>