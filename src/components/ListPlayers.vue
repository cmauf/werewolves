<template>
    <div class="playerlist">
        <h2>{{ headline }}</h2>
		<AddData v-on:dataToAdd="addPlayer" />
		<ul>
			<li v-bind:key="player.id" v-for="player in players">
				<span>{{ player.name }}{{ showRole(player) }}</span><label class="rm-btn" v-on:click="$emit('remove-player', player.id)"><img src="../assets/criss-cross-24px.png" margin-left="20 px" width="16px" heigth="16px" padding="1px"></label>
			</li>
		</ul>
    </div>
</template>

<script>
import AddData from './AddData.vue'

export default {
	name: 'ListPlayers',
	components: {
		AddData
	},
    data() {
		return {
			newplayer: '',
			headline: 'Mitspieler*innen',
			nextID: 1
		}
	},
	methods: {
		addPlayer(NewPlayer) {
		if (NewPlayer > '') {
			const playerToAdd = {
				id: this.nextID,
				name: NewPlayer,
				role: 'none'
			}
			this.$emit('new-player', playerToAdd);
			this.newplayer = '';
			this.nextID++;
			}
		
		},
		removePlayer(playerID) {
			this.$emit('remove-player', playerID);
		},
		showRole(player) {
		if (player.role != 'none') return ", " + player.role;
		else return '';
		},
		sortNames(e) { //not working as intended yet
			e.preventDefault();
			var newplayers = this.players;
			for (let i = newplayers.length; i> 0; i--) {
				for (let j = 0; j < newplayers.length-2; j++) {
					var a = newplayers[j];
					var b = newplayers[j+1];
					if (this.ascending(a.name, b.name) == 1) {
						newplayers.$set(j, b);
						newplayers.$set(j+1, a);
					}
				}
			}
			this.players = newplayers;
		},
		ascending: function(a, b) { //courtesy of d3.array
			return a < b ? -1 : a > b ? 1 : a >= b ? 0 : NaN;
		}
	},
	props: [
		'players',
		]
		
}
</script>

<style scoped>
form {
	height: 40px;
	padding: 10px;
 }
input{
	display: inline-block;
	width: 85%;
	margin-right: 5px;
}
span{
	display: inline-block;
	width: 90%;
}
</style>