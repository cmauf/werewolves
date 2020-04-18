<template>
    <div>
        <h1>Spielleiter*innensicht</h1>
        <div v-bind:key="player.id" v-for="player in this.players">
                {{ player.name }}
                {{ player.role }}  
        </div>
        <button @click="endGame">Spiel beenden</button><button @click="initiate">LOS</button>
    </div>
</template>

<script>
export default {
    name: 'GameLoop',
    data: function() {
        return {
           gameInstance: [],
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
    methods: {
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
        initiate: function() {
            let player;
            for (player in this.players) {
                console.log('Evaluating ' + player);
                const newPlayer = {
                id: player[0],
                name: player[1],
                role: player[2],
                roleIMG: this.getImgURL(player[2]),
                dead: false
                }
                console.log('name: ' + newPlayer.name + ', id: ' + newPlayer.id + ' rolle: ' + newPlayer.role + ' bild: ' + newPlayer.roleIMG);
                this.gameInstance = [...this.gameInstance, newPlayer];
            }
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