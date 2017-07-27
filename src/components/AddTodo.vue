<template>
	<div>
		<fieldset>
			<legend>Add To-Do</legend>
			<div>To-Do</div>
			<input class="input" type="text" v-model="todoValue">
			<button class="button" v-on:click="cancel">Cancel</button>
			<button class="button" v-on:click="create">Create</button>
		</fieldset>
	</div>
</template>


<script>
import axios from 'axios';
var root = 'https://jsonplaceholder.typicode.com';

export default {
	props: ['user'],
	data() {
		return {
			todoValue: ''
		};
	},
	methods: {
		cancel: function() {
			this.todoValue = '';
			this.$emit('close');
		},
		create: function() {
			if(this.todoValue != '') {
				axios.post(root + '/todos', {
					completed: false,
					title: this.todoValue,
					userId: this.user.id
				}).then(res => {
					this.todoValue = '';
					this.$emit('close', res.data);
				});
			}
		}
	}
}
</script>


<style scoped>
	fieldset {
		width: 500px;
		padding: 30px;
		margin: 40px auto 0;
	}
	fieldset legend {
		font-family: sans-serif;
		font-size: .9em;
	}
	.input {
		margin-top: 10px;
		width: 100%;
	}
	.button {
		width: 80px;
		padding: 5px;
		margin-top: 20px;
	}
</style>
