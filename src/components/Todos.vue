<template>
	<div>
		<div class="top-bar">
			<div>Welcome, {{user && user.name}}</div>
			<button v-show="!addTodoActive" v-on:click="addTodo">Add To-do</button>
		</div>
		<AddTodo v-show="addTodoActive" v-on:close="closeAddTodo" :user="user"></AddTodo>
		<hr>
		
		<h4>To-Dos</h4>
		<ul>
			<li v-for="todo in todos" v-if="!todo.completed">{{todo.title}}</li>
		</ul>
		
		<h4>Completed</h4>
		<ul>
			<li v-for="todo in todos" v-if="todo.completed">{{todo.title}}</li>
		</ul>

	</div>
</template>


<script>
import AddTodo from './AddTodo';

import axios from 'axios';
var root = 'https://jsonplaceholder.typicode.com';

export default {
	props: ['user'],
	watch: {
		user: function() {
			this.refreshTodos();
		}
	},
	data() {
		return {
			addTodoActive: false,
			todos: []
		};
	},
	components: {
		AddTodo
	},
	methods: {
		addTodo: function() {
			this.addTodoActive = true;
		},
		closeAddTodo: function(newTodo) {
			this.addTodoActive = false;
			if(newTodo) {
				// add new todo item to the list:
				this.todos.push(newTodo);
				// this would be better and more safe approach:
				//this.refreshTodos();
			}
		},
		refreshTodos: function() {
			axios.get(root + '/todos?userId=' + this.user.id).then(res => {
				this.todos = res.data;
			});
		}
	}
}
</script>


<style scoped>
	.top-bar {
		text-align: right;
	}
	.top-bar button {
		margin-top: 20px;
		padding: 5px;
		width: 100px;
	}
</style>
