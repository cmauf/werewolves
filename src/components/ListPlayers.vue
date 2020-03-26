<template>
    <div class="playerlist">
        {{ headline }}:
		<form @submit="addPlayer">
			<input type="text" v-model="newplayer"><button type="submit">Hinzufügen</button>
		</form>
		<ul>
			<li v-bind:key="player.id" v-for="player in players">{{ player.name }}<span >{{ showRole(player) }}</span></li>
		</ul>
    </div>
</template>

<script>


export default {
	name: 'ListPlayers',
    data() {
		return {
			newplayer: '',
			headline: 'Mitspieler*innen',
			nextID: 1
		}
	},
	methods: {
		addPlayer(e) {
		e.preventDefault();
		if (this.newplayer > '') {
			const playerToAdd = {
				id: this.nextID,
				name: this.newplayer,
				role: 'none'
			}
			this.$emit('new-player', playerToAdd);
			this.newplayer = '';
			this.nextID++;
			}
		
		},
		showRole(player) {
		if (player.role != 'none') return ", " + player.role;
		else return '';
		}
	},
	props: [
		'players',
		]
		
}
</script>

<style>

</style>