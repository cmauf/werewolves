<template>
    <div>
        <h1>Spielleiter*innensicht</h1>
        <div v-if="!this.looping">
            <ul>
                <li v-bind:key="player.id" v-for="player in this.players">
                {{ player.name }}
                {{ player.role }} 
                </li>
            </ul>
        </div>
        <div v-else class="game-grid">
            <div v-for="player in this.gameInstance" v-bind:key="player.id" 
            :id="player.id" :class="!player.dead ? dead : alive" class="grid-item" @click="player.dead = !player.dead">
                <div>
                    <img :src="'/img/' + player.roleIMG" class="role-image"/>
                </div>
                <div>
                    <h2>{{ player.name }}</h2>
                    <p>{{ player.role }}</p>
                    <p><span v-if="!player.dead">lebendig</span><span v-else style="font-color: red">tot</span></p>
                </div>
            </div>
        </div>
        <button @click="endGame">Spiel beenden</button><button @click="initiate" v-if="!looping">LOS</button>
    </div>
</template>

<script>
export default {
    name: 'GameLoop',
    data: function() {
        return {
            gameInstance: [],
            looping: false,
            recommendedRoles: [
                'Bewohner', 'Bewohner', 'Bewohner', 'Bewohner', 'Bewohner',
                'Seher', 'Werwolf1', 'Werwolf2', 'Medium', 'Besessener',
                'Bannweberin', 'Liebender', 'Liebende', 'Hexe', 'Werwolf3',
                'Thaumaturgin', 'Verfluchter', 'Werhamster', 
                'Bewohner', 'Bewohner', 'Kleines Mädchen', 'Bewohner', 'Zäher Hund'
            ],
            roleURLs: [
                {name: 'Werwolf1', url: 'werwolf1.png'},
                {name: 'Werwolf2', url: 'werwolf2.png'},
                {name: 'Werwolf3', url: 'werwolf3.png'},
                {name: 'Seher', url:'seher.png'},
                {name: 'Medium', url: 'medium.png'},
                {name: 'Besessener', url: 'besessener.png'},
                {name: 'Liebender', url: 'liebender.png'},
                {name: 'Liebende', url: 'liebende.png'},
                {name: 'Hexe', url: 'hexe.png'},
                {name: 'Thaumaturgin', url: 'thaumaturgin.png'},
                {name: 'Verfluchter', url: 'verfluchter.png'},
                {name: 'Werhamster', url: 'werhamster.png'},
                {name: 'Kleines Mädchen', url: 'kleines-maedchen.png'},
                {name: 'Zäher Hund', url: 'zaeher-hund.png'}
            ],
            villagers: [
                'bewohner1.png',
                'bewohner2.png',
                'bewohner3.png',
                'bewohner4.png',
            ]
        }
    },
    methods: {
        endGame() {
            this.looping = false;
            this.$emit('endGame');
        },
        getImgURL: function(str) {
            if (str == 'Bewohner') {
                const i = Math.floor(Math.random() * (4));
                return this.villagers[i];
            }
            else if(str == 'Werwolf') {
                const i = Math.floor(Math.random() * (3));
                return this.roleURLs[i].url;
            }
            else{
                for (let index in this.roleURLs) {
                    console.log('Checking ' + this.roleURLs[index].name, 'comparing with ' + str);
                    if (this.roleURLs[index].name.toLowerCase() == str.toLowerCase()){
                        console.log('Found ' + this.roleURLs[index].name);
                        return this.roleURLs[index].url;
                    }
                }
            }
            return 'nar.png';
        },
        initiate: function() {
            for (let index in this.players) {
                console.log('Evaluating ' + this.players[index]);
                const newPlayer = {
                    id: this.players[index].id,
                    name: this.players[index].name,
                    role: this.players[index].role,
                    roleIMG: this.getImgURL(this.players[index].role),
                    dead: false
                }
                console.log('name: ' + newPlayer.name + ', id: ' + newPlayer.id + ' rolle: ' + newPlayer.role + ' bild: ' + newPlayer.roleIMG);
                this.gameInstance = [...this.gameInstance, newPlayer];
            }
            this.looping = true;
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
    .game-grid{
        display: grid;
        grid-template-columns: auto auto auto auto;
    }
    .grid-item{
        padding: 10px;
        display: flex;

    }
    .role-image{
        max-width: 80%;
        height: auto;
        

    }

</style>