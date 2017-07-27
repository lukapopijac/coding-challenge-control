<template>
	<div>
		<Login v-show="!loggedIn" v-on:success-login="successLogin"></Login>
		<Todos v-show="loggedIn" :user="user"></Todos>
	</div>
</template>

<script>
import Login from './components/Login';
import Todos from './components/Todos';

export default {
	data() {
		return {
			loggedIn: false,
			user: null
		};
	},
	components: {
		Login,
		Todos
	},
	methods: {
		successLogin: function(user) {
			this.loggedIn = true;
			this.user = user;
		}
	}
}
</script>

<style scoped>
</style>