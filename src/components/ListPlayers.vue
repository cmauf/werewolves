<template>
    <div class="playerlist">
        <h2>{{ headline }}</h2>
		<form @submit="addPlayer">
			<input type="text" v-model="newplayer"><label id="add-btn" v-on:click="addPlayer"><img src="../assets/plus-24px.png" margin-left="20 px" width="16px" heigth="16px" padding="1px"></label>
		</form>
		<ul>
			<li v-bind:key="player.id" v-for="player in players">
				<span>{{ player.name }}{{ showRole(player) }}</span><label class="rm-btn" v-on:click="$emit('remove-player', player.id)"><img src="../assets/criss-cross-24px.png" margin-left="20 px" width="16px" heigth="16px" padding="1px"></label>
			</li>
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
		removePlayer(playerID) {
			this.$emit('remove-player', playerID);
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