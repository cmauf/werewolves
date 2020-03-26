<template>
  <div id="app">
    <h1>Marc's Fabulöse Werwolf-Rollenverteilung</h1>
	<div class="playerlist">
		<ListPlayers v-on:new-player="addPlayer"/>
		
	</div>
	<button v-on:click="fillRoleQueue">Rollen-Queue füllen</button>
	<button v-on:click="makeRoles">Rollen verteilen</button>
	<div class="rolelist">
		<ListRoles />
		<ul>
			<li v-bind:key="role.qty" v-for="role in roles">{{ role.name }}, Anzahl <span v-on:click="role.qty--">-</span> {{ role.qty  }} <span v-on:click="role.qty++">+</span></li>
		</ul>
	</div>
  </div>
</template>

<script>
import ListPlayers from './components/ListPlayers.vue'
import ListRoles from './components/ListRoles.vue'

export default {
  name: 'App',
  components: {
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
		{name: 'Seherin', qty: 0},
		{name: 'Hexe', qty: 0},
		{name: 'Werwolf', qty: 0},
		{name: 'Bürger', qty: 0},
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
	makeRoles(e) {
		e.preventDefault();
		this.fillRoleQueue();
		var player;
		for(player in this.players){
			if (this.roleQueue.length == 0) {
				alert('Zu wenig Rollen für die Spieler!')
				break;
			}
			player.role = this.roleQueue.splice(Math.floor(Math.random()*this.roleQueue.length), 1);
		}
		if (this.roleQueue.length > 0) {
			alert("Zu viele Rollen für die Spieler*innen");
		}
	},
	fillRoleQueue: function(e) {
		e.preventDefault();
		var role;
		for (role in this.roles) {
			for (var i = role.qty; i>0; i--) {
			this.roleQueue.push(role.name);
			}
		}
	},
	showRole(player) {
		if (player.role != 'none') return ", " + player.role;
		else return '';
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
