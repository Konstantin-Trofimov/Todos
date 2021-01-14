<template>
	<div>
		<h2>Todo app</h2>
		<router-link to="/">Home</router-link>
		<hr>
		<AddTodo @add-todo="addTodo" />
		<select v-model="filter">
			<option value="all">All</option>
			<option value="completed">Completed</option>
			<option value="not-completed">No completed</option>
		</select>
		<hr>
		<Loader v-if="loading"/>
		<TodoList 
		class="list"
		v-else-if="filteredTodos.length" 
		v-bind:todos="filteredTodos" 
		@remove-todo="removeTodo" />

		<p v-else>No todos</p>
	</div>
</template>

<script>
	import TodoList from '@/components/TodoList'
	import AddTodo from '@/components/AddTodo'
	import Loader from '@/components/Loader'


	export default {
		name: 'App',
		data() {
			return {
				todos: [],
				loading: true,
				filter: 'all'
			}
		},
		mounted() {
			fetch('https://jsonplaceholder.typicode.com/todos?_limit=10')
				.then(response => response.json())
				.then(json => {
					this.todos = json
					this.loading = false
			})
		},
		// watch: {
		// 	filter(value) {
		// 		console.log(value)
		// 	}
		// },
		computed: {
			filteredTodos() {
				if (this.filter === 'all') {
					return this.todos
				} 

				if (this.filter === 'completed') {
					return this.todos.filter(t => t.completed)
				}

				if (this.filter === 'not-completed') {
					return this.todos.filter(t => !t.completed)
				}
			}
		},
		methods: {
			removeTodo(id) {
				this.todos = this.todos.filter(t => t.id !== id)
			},
			addTodo(todo) {
				this.todos.push(todo)
			}
		},
		components: {
			TodoList,
			AddTodo,
			Loader
		}
	}
</script>

<style>
	.list {
		display: flex;
		flex-direction: column;
		align-items: center;
	}

	select {
		margin-top: 1.5rem;
		height: 1.7rem;
		border-radius: .3rem;
		border-color: #ccc;
		padding-left: .5rem;
	}

	select:focus {
		outline: none;
	}
</style>