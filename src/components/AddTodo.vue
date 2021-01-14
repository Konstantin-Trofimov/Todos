<template>
	<form @submit.prevent="onSubmit">
		<input type="text" v-model="title">
		<button type="submit">Create</button>
	</form>
</template>

<script>
	export default {
		data() {
			return {
				title: ''
			}
		},
		methods: {
			onSubmit() {
				if (this.title.trim()) {
					const newTodo = {
						id: Date.now(),
						title: this.title,
						completed: false
					}

					this.$emit('add-todo', newTodo)
					this.title = ''
				}
			}
		}
	}
</script>

<style scoped>
	form {
		justify-content: center;
		display: flex;
	}

	input {
		width: 300px;
		height: 2.5rem;
		padding-left: 30px;
		font-size: 16px;
		border-radius: .5rem 0 0 .5rem;
		border-color: #ccc;
	}

	input:focus, button:focus {
		outline: none;
	}

	button {
		width: 5rem;
		background: rgb(57, 106, 211);
		color: #fff;
		font-weight: bold;
		font-size: 18px;
		border: none;
		border-radius: 0 .5rem .5rem 0;
		cursor: pointer;
		transition: .6s;
	}

	button:hover {
		background: rgb(65, 121, 242);
	}

</style>