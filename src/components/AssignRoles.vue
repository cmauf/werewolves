<template>
    <div>
        <h2>Funktionen</h2>
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
            if (roleQueue.length !=  this.players.length) {
                    alert('Rollen und Spieler sind nicht identisch')
                    return 0;
                }
            var player;
            var i = this.players.length-1;
            for(player in this.players){
                    this.players[player].role = roleQueue[i];
                    i--;
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
            roleQueue = this.shuffle(roleQueue);
            this.rolesQueue = roleQueue;
            return roleQueue;
            },
        shuffle(a) {
            for (let i = a.length - 1; i > 0; i--) {
            const j = Math.floor(Math.random() * (i + 1));
            [a[i], a[j]] = [a[j], a[i]];
            }
            return a;
        }
            
        },
    props: [
        'players',
        'roles'
        ]
        
}
</script>

<style scoped>

</style>