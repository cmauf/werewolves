<template>
	<div class="rolelist">
		<h2>{{ headline }}</h2>
		<ul>
			<li v-bind:key="role.name" v-for="role in roles"><span class="rolename">{{ role.name }}</span><label v-on:click="decrease(role)"><img src="../assets/minus-24px.png" margin-left="20 px" width="16px" heigth="16px" padding="1px"></label> {{ role.qty  }} <label v-on:click="role.qty++"><img src="../assets/plus-24px.png" margin-left="20 px" width="16px" heigth="16px" padding="1px"></label></li>
		</ul>
	</div>
</template>

<script>

export default {
    name: 'ListRoles',
	data() {
		return {
			headline: 'Rollen'
		}
	},
	methods: {
		decrease: function(a) {
			if(a.qty > 0) a.qty--;
		}
	},
	props: [
		"roles"
		]
}
</script>

<style scoped>
	span {
		display: inline-block;
		margin-right: 10px;
		width: 70%;
	}
	
	@media only screen and (min-width: 800px) {
		ul{
			margin-top: 60px;
		}
}
</style>