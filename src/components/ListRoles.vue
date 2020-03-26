<template>
	<div class="rolelist">
		{{ headline }}:
		<ul>
			<li v-for="role in rolelist" v-bind:key="role.name"></li>
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