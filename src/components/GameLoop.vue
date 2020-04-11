<template>
    <div>
        <h1>Spielleiter*innensicht</h1>
        <div v-bind:key="player.id" v-for="player in players" >
                {{ player.name }}
                {{ player.role }}
                
        </div>
        <button @click="makeRoles">Rollen verteilen</button><button @click="endGame">Spiel beenden</button><button @click="initiate">LOS</button>
    </div>
</template>

<script>
export default {
    name: 'GameLoop',
    data() {
        return {
            recommendedRoles: [
                'Bewohner', 'Bewohner', 'Bewohner', 'Bewohner', 'Bewohner',
                'Seher', 'Werwolf1', 'Werwolf2', 'Medium', 'Besessener',
                'Bannweberin', 'Liebender', 'Liebende', 'Hexe', 'Werwolf3',
                'Thaumaturgin', 'Verfluchter', 'Werhamster', 
                'Bewohner', 'Bewohner', 'Kleines Mädchen', 'Bewohner', 'Zäher Hund'
            ],
            roleURLs: [
                {name: 'Werwolf1', url: '../assets/werwolf1.png'},
                {name: 'Werwolf2', url: '../assets/werwolf2.png'},
                {name: 'Werwolf3', url: '../assets/werwolf3.png'},
                {name: 'Seher', url:'../assets/seher.png'},
                {name: 'Medium', url: '../assets/medium.png'},
                {name: 'Besessener', url: '../assets/besessener.png'},
                {name: 'Liebender', url: '../assets/liebender.png'},
                {name: 'Liebende', url: '../assets/liebende.png'},
                {name: 'Hexe', url: '../assets/hexe.png'},
                {name: 'Thaumaturgin', url: '../assets/thaumaturgin.png'},
                {name: 'Verfluchter', url: '../assets/verfluchter.png'},
                {name: 'Werhamster', url: '../assets/werhamster.png'},
                {name: 'Kleines Mädchen', url: '../assets/kleines-maedchen.png'},
                {name: 'Zäher Hund', url: '../assets/zaeher-hund.png'}
            ],
            villagers: [
                '../assets/bewohner1.png',
                '../assets/bewohner2.png',
                '../assets/bewohner3.png',
                '../assets/bewohner4.png',
            ]
        }
    },
    computed: {
        gameInstance: function() {
            var instance = [];
            var player;
            for (player in this.players) {
                let newName = player.name;
                let newID = player.id;
                let newRole = player.role;
                let newImgURL = this.getImgURL(newName);
                const newPlayer = {
                    name: newName,
                    id: newID,
                    role: newRole,
                    roleIMG: newImgURL,
                    dead: false
                }
            instance = [...instance, newPlayer]
            }
            return instance;
        }
    },
    methods: {
        addPlayer: function(player) {
            const newPlayer = {
                name: player.name,
                id: player.id,
                role: player.role,
                roleIMG: this.getURLforInstance(player.role),
                dead: false
            }
            console.log('name: ' + newPlayer.name + ', id: ' + newPlayer.id + ' rolle: ' + newPlayer.role + ' bild: ' + newPlayer.roleIMG);
            return newPlayer
        },
        endGame() {
            this.$emit('endGame');
        },
        getImgURL: function(str) {
            if (str == 'Bewohner') {
                const i = Math.floor(Math.random() * (4));
                return this.villagers[i];
            }
            var instance;
            for (instance in this.roleURLs) {
                if (instance.name == str){
                    return instance.url;
                }
            }
            return '../assets/nar.png';
        },
        getURLforInstance: function(str) {
            if (str == 'Bewohner') {
                const i = Math.floor(Math.random() * (4));
                return this.villagers[i];
            }
            var instance;
            for (instance in this.roleURLs) {
                if (instance.name == str){
                    return instance.url;
                }
            }
            return '../assets/nar.png';
        },
        makeGameCard: function(player) {
            var newPlayer = this.addPlayer(player)
            this.gameInstance = [...this.gameInstance, newPlayer]
        },
        makeRoles: function(e) {
            e.preventDefault();
            this.players = this.shuffle(this.players);
            var player;
            var i = 0;
            for (player in this.players) {
                console.log('evaluating' + player.id);
                player.role = this.recommendedRoles[i];
                console.log('Assigned '+ player.role);
                this.makeGameCard(player);
                i++;
            }
        },
        shuffle: function(a) {
            for (let i = a.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [a[i], a[j]] = [a[j], a[i]];
            }
            return a;
        },
        toggleDead: function(player) {
            player.dead=!player.dead
        }
    },
    props: [
        'players'
    ]
    
}
</script>

<style scoped>

</style>