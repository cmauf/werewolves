<template>
  <div id="app">
		<div v-if="!screenOn">
			<h1>Marcs Fabulöse Werwolf-Rollenverteilung</h1>
			<div class="row">
				<div class="column">
					<ListPlayers v-bind:players="players" v-on:new-player="addPlayer" v-on:remove-player="removePlayer"/>
				</div>
				
				<div class="column">
					<ListRoles v-bind:roles="roles" v-on:addRole="updateRoles"/>
				</div>

				<div class="column">
					<Functions v-bind:players="players" v-bind:roles="roles" v-on:makeScreen="toggleGame"/>
				</div>
			</div>
		</div>
		<div v-else>
			<GameLoop v-bind:players="players" v-on:endGame="toggleGame" />
		</div>
  </div>
</template>

<script>
import ListPlayers from './components/ListPlayers.vue'
import ListRoles from './components/ListRoles.vue'
import Functions from './components/Functions.vue'
import GameLoop from './components/GameLoop.vue'

export default {
  name: 'App',
  components: {
	Functions,
	GameLoop,
	ListPlayers,
	ListRoles
  },
  data() {
	return {
		players: [
			{name: 'Anna', role: 'none', id: 1},
			{name: 'Berta', role: 'none', id: 2},
			{name: 'Caro', role: 'none', id: 3},
			{name: 'Daniel', role: 'none', id: 4},
			{name: 'Erich', role: 'none', id: 5},
			{name: 'Frieder', role: 'none', id: 6},
			{name: 'Getrude', role: 'none', id: 7},
			{name: 'Hellmuth', role: 'none', id: 8},
		],
		roles: [
		{name: 'Bewohner', qty: 4},
		{name: 'Werwolf', qty: 1},
		{name: 'Seherin', qty: 1},
		{name: 'Hexe', qty: 1},
		{name: 'Armor', qty: 1}
		],
		screenOn: false
	}
  },
  methods: {
	addPlayer(newPlayer) {
		this.players = [...this.players, newPlayer];
	},
	toggleGame() {
		this.screenOn = !this.screenOn;
	},
	showRole(player) {
		if (player.role != 'none') return ", " + player.role;
		else return '';
	},
	removePlayer(playerID) {
		this.players = this.players.filter(player => player.id != playerID);
	},
	updateRoles(newRole){
		this.roles = [...this.roles, newRole];
	}
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.row {
  display: flex;
  margin: 20px;
  padding: 10px;
}
.row:after {
  content: "";
  display: table;
  clear: both;
}
.column {
  width: 33%;
  padding: 10px;
}
@media screen and (max-width: 800px) {
  .row{
	display: block;
  }
  .column {
    width: 100%;
  }
}


h2 {
  font: 300 30px/1.5 Helvetica, Verdana, sans-serif;
  margin: 0;
  padding: 0;
}

ul {
  list-style-type: none;
  margin-top: 0;
  text-align: left;
}
 
li {
  font: 200 20px/1.5 Helvetica, Verdana, sans-serif;
  border-bottom: 1px solid #ccc;
}
 
li:last-child {
  border: none;
}
 
</style>
