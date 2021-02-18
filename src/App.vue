<template>
  <div id="app">
		<div v-if="!screenOn">
			<h1>Fabulöse Werwolf-Rollenverteilung</h1>
			<div class="row">
				<div class="column">
					<ListPlayers />
				</div>
				
				<div class="column">
					<ListRoles />
				</div>

				<div class="column">
					<Functions v-on:makeScreen="toggleGame"/>
				</div>
			</div>
		</div>
		<div v-else>
			<GameLoop v-on:endGame="toggleGame" />
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
		screenOn: false
	}
  },
  methods: {
	toggleGame() {
		this.screenOn = !this.screenOn;
	}
  },
  beforeDestroy() {
	this.$emit(this.players)
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
