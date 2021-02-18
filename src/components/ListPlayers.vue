<template>
    <div class="playerlist">
        <h2>{{ headline }}</h2>
		<AddData v-on:dataToAdd="addPlayer" />
		<ul>
			<li v-bind:key="player.id" v-for="player in players">
				<span>{{ player.name }}{{ showRole(player) }}</span>
				<label class="rm-btn" @click="removePlayer(player.id)">
					<img src="../assets/criss-cross-24px.png" class="deletePlayer">
				</label>
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
      nextID: 9,
      players: [
        {name: 'Anna', role: 'none', id: 1},
        {name: 'Buraq', role: 'none', id: 2},
        {name: 'Caro', role: 'none', id: 3},
        {name: 'Daniel', role: 'none', id: 4},
        {name: 'Erich', role: 'none', id: 5},
        {name: 'Florence', role: 'none', id: 6},
        {name: 'Getrude', role: 'none', id: 7},
        {name: 'Hakan', role: 'none', id: 8},
      ],
		}
  },
	methods: {
		addPlayer(newPlayer) {
		if (newPlayer > '') {
			const playerToAdd = {
				id: this.nextID,
				name: newPlayer,
				role: 'none'
			}
			this.players = [...this.players, playerToAdd]
			this.newplayer = '';
			this.nextID++;
			}
		
		},
		removePlayer(playerID) {
			this.players = this.players.filter(player => player.id != playerID)
		},
		showRole(player) {
      if (player.role != 'none') return ", " + player.role;
      else return ''
		}
	}
		
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
.deletePlayer {
  margin-left: 20px;
  width: 16px; 
  height: 16px; 
  padding: 1px;
}
</style>