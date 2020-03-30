<template>
    <form @submit="addData">
			<input type="text" v-model="newdata">
            <label id="add-btn" v-on:click="addData"><img src="../assets/plus-24px.png" id="plussign"></label>
		</form>
</template>

<script>
export default {
    data() {
        return {
            newdata: ''
        }
    },
    methods: {
        addData: function(e) {
            e.preventDefault();
            this.$emit("dataToAdd", this.newdata);
            this.newdata = '';
        }
    }
    
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
.add-btn {
    margin-left: 20 px;
    margin-top: 2px;
    padding: 1px;
}
#plussign {
    height: 16px;
    width: 16px;

}
</style>