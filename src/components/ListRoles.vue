<template>
	<div class="rolelist">
		{{ headline }}:
		<ul>
			<li v-bind:key="role.name" v-for="role in roles">{{ role.name }}, Anzahl <span v-on:click="role.qty--">-</span> {{ role.qty  }} <span v-on:click="role.qty++">+</span></li>
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
	props: [
		"roles"
		]
}
</script>

<style>

</style>