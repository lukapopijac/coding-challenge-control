<template>
	<div>
		<div class="box">
			<h2>LOGIN TO VIEW OR ADD TO-DOS</h2>
			<div>Usename</div>
			<div class="error">{{errorMessage}}</div>
			<input class="input" type="text" v-model="username" v-on:input="onInput">
			<button class="submit" v-on:click="submit">Log In</button>
		</div>
	</div>
</template>

<script>
import axios from 'axios';
var root = 'https://jsonplaceholder.typicode.com';

export default {
	data() {
		return {
			username: '',
			errorMessage: ''
		};
	},
	methods: {
		submit: function() {
			axios.get(root + '/users?username=' + this.username).then(res => {
				let data = res.data;
				if(data.length==0) this.errorMessage = 'Invalid username';
				else this.$emit('success-login', res.data[0]);
			});
		},
		onInput: function() {
			this.errorMessage = '';
		}
	}
}
</script>


<style scoped>
	h2 {
		font-size: 1.3em;
		text-align: center;
		font-family: sans-serif;
		margin-bottom: 40px;
		font-weight: normal;
	}
	.box {
		border: 1px solid black;
		width: 500px;
		padding: 30px;
		margin: 40px auto 0;
	}
	.input {
		margin-top: 10px;
		width: 100%;
	}
	.submit {
		width: 80px;
		padding: 5px;
		margin-top: 20px;
	}
	.error {
		color: red;
	}
</style>
