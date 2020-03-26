<template>
  <div id="app">
    <h1>Marc's Fabulöse Werwolf-Rollenverteilung</h1>
	<div class="playerlist">
		<ListPlayers v-bind:players="players" v-on:new-player="addPlayer" v-on:remove-player="removePlayer"/>
	</div>
	<div class="roleassign">
		<AssignRoles v-bind:players="players" v-bind:roles="roles" />
	</div>
	<div class="rolelist">
		<ListRoles v-bind:roles="roles"/>

	</div>
  </div>
</template>

<script>
import ListPlayers from './components/ListPlayers.vue'
import ListRoles from './components/ListRoles.vue'
import AssignRoles from './components/AssignRoles.vue'

export default {
  name: 'App',
  components: {
	AssignRoles,
	ListPlayers,
	ListRoles
  },
  data() {
	return {
		newplayer: '',
		players: [
			{id: 0, name: 'Test', role: 'Bürger'}
		],
		roles: [
		{name: 'Bürger', qty: 0},
		{name: 'Werwolf', qty: 0},
		{name: 'Seherin', qty: 0},
		{name: 'Hexe', qty: 0},
		{name: 'Armor', qty: 0}
		],
		roleQueue: [
		]
	}
  },
  methods: {
	addPlayer(newPlayer) {
		this.players = [...this.players, newPlayer];
	},
	updateQty(e) {
		e.preventDefault();
		const updated = +e.innerHTML.getElementById('newqty');
		this.player.qty = updated;
	},
	showRole(player) {
		if (player.role != 'none') return ", " + player.role;
		else return '';
	},
	removePlayer(playerID) {
		this.players = this.players.filter(player => player.id != playerID);
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
.playerlist {
	float: left;
}
.rolelist {
	float: right;
}
</style>
