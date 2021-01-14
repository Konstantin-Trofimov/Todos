<template>
	<li>
		<span v-bind:class="{done: todo.completed}">
			<input 
			type="checkbox" 
			v-on:change="todo.completed = !todo.completed">
			<strong>{{index + 1}}</strong>
			{{todo.title | uppercase}}
		</span>
		<button 
		class="rm"
		v-on:click="$emit('remove-todo', todo.id)"
		>&times;
		</button>
	</li>
</template>

<script>
	export default {
		props: {
			todo: {
				type: Object,
				required: true
			},
			index: Number
		}, 
		filters: {
			uppercase(value) {
				return value.toUpperCase()
			}
		}
	}
</script>

<style scoped>

	span {
		text-align: start;
	}

	li {
		max-width: 600px;
		border: 1px solid #ccc;
		display: grid;
		grid-template-columns: 1fr .02fr;
		column-gap: 1rem;
		padding: .5rem 2rem;
		margin-bottom: 1rem;
		align-items: center;
	}

	.rm {
		background:  rgb(181, 26, 26);
		color: #fff;
		border-radius: 50%;
		font-weight: bold;
		border: none;
		cursor: pointer;
		transition: .6s;
		width: 1.5rem;
		height: 1.5rem;
		text-align: center;
		
	}

	.rm:hover {
		background: rgba(181, 26, 26, 0.81);
	}

	.rm:focus {
		outline: none;
	}

	.done {
		text-decoration-line: line-through;
	}

	input {
		margin-right: 1rem;
		cursor: pointer;
	}

</style>