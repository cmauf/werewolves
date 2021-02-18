<template>
	<div class="rolelist">
		<h2>{{ headline }}</h2>
		<AddData v-on:dataToAdd="addRole" />
		<ul>
			<li v-bind:key="role.name" v-for="role in roles">
        <span class="rolename">{{ role.name }}</span>
        <label v-on:click="decrease(role)">
          <img src="../assets/minus-24px.png" margin-left="20 px" width="16px" heigth="16px" padding="1px">
        </label> {{ role.qty  }} 
        <label v-on:click="role.qty++">
          <img src="../assets/plus-24px.png" margin-left="20 px" width="16px" heigth="16px" padding="1px">
        </label>
      </li>
		</ul>
	</div>
</template>

<script>
import AddData from './AddData.vue'

export default {
	name: 'ListRoles',
	components:{
		AddData
	},
	data() {
		return {
      headline: 'Rollen',
      roles: [
        {name: 'Bewohner', qty: 4},
        {name: 'Werwolf', qty: 1},
        {name: 'Seherin', qty: 1},
        {name: 'Hexe', qty: 1},
        {name: 'Armor', qty: 1}
      ],
		}
	},
	methods: {
		decrease(a) {
			if(a.qty > 0) a.qty--;
		},
		addRole(newRole) {
			if (newRole > '') {
				const roleToAdd = {
					name: newRole,
					qty: 0
				}
				this.roles = [...this.roles, roleToAdd]
			}
			
		}
	}
}
</script>

<style scoped>
	span {
		display: inline-block;
		margin-right: 10px;
		width: 70%;
	}

</style>
