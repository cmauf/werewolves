<template>
    <div>
        <h2>Funktionen</h2>
        <button v-on:click="makeRoles">Rollen verteilen</button>
        <button @click="sortPlayersByName">Spieler*innenliste alphabetisch nach Namen sortieren</button>
        <button @click="sortPlayersByRole">Spieler*innenliste alphabetisch nach Rollen sortieren</button>
    </div>
</template>

<script>
export default {
    name: 'Functions',
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
        },
        sortPlayersByName() {
            this.players.sort((a,b) => a.name.toUpperCase() > b.name.toUpperCase())
        },
        sortPlayersByRole () {

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