<template>
  <div id="app">
    <h1>Marcs Fabulöse Werwolf-Rollenverteilung</h1>
	<div class="row">
	<div class="column">
		<ListPlayers v-bind:players="players" v-on:new-player="addPlayer" v-on:remove-player="removePlayer"/>
	</div>
	
	<div class="column">
		<ListRoles v-bind:roles="roles" v-on:addRole="updateRoles"/>
	</div>

	<div class="column">
		<Functions v-bind:players="players" v-bind:roles="roles" />
	</div>
	</div>
  </div>
</template>

<script>
import ListPlayers from './components/ListPlayers.vue'
import ListRoles from './components/ListRoles.vue'
import Functions from './components/Functions.vue'

export default {
  name: 'App',
  components: {
	Functions,
	ListPlayers,
	ListRoles
  },
  data() {
	return {
		newplayer: '',
		players: [
		],
		roles: [
		{name: 'Bürger', qty: 0},
		{name: 'Werwolf', qty: 0},
		{name: 'Seherin', qty: 0},
		{name: 'Hexe', qty: 0}
		],
		roleQueue: [
		]
	}
  },
  methods: {
	addPlayer(newPlayer) {
		this.players = [...this.players, newPlayer];
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
  flex: 100%;
}
@media only screen and (min-width: 800px) {
  .column {
    flex: 33%;
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
