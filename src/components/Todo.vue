<template>
	<div v-bind:class="{ 'completed': todo.completed }" v-on:click="markComplete" class="todo">
		<p>{{ todo.title }}</p>
		<button @click="$emit('delete-todo', todo.id)"></button>
	</div>
</template>
<script>
export default {
	name: 'Todo',
	props: [
		"todo"
	],
	methods: {
		markComplete() {
			const completedTodo = {
				id: this.todo.id,
				title: this.todo.title,
				completed: !this.todo.completed
			};
			this.todo.completed = !this.todo.completed;
			this.$emit('completed-todo', completedTodo);
		}
	}
}
</script>
<style scoped>
	.todo{
		display: flex;
		justify-content: space-between;
		align-items: center;
		border-radius: 5px;
		padding: 0 1em;
		background-color: #f6e1a0;
		box-shadow: -10px 10px 0 0 rgba(34, 60, 80, 0.1);
		margin-bottom: 1em;
		transition: all 0.5s ease-in-out;
		line-break: anywhere;
	}
	.todo p{
		margin-right: 1em;
		width: 80%;
	}
	.completed {
		background-color: #aaaaaa;
	}
	.completed p{
		text-decoration: line-through;
	}
	button{
		border: none;
		border-radius: 5px;
		/*background-color: #fc5e5e;*/
		background: url("../assets/delete.svg") no-repeat center center #fc5e5e;
		background-size: 70%;
		height: 25px;
		width: 25px;
		/*color: #373737;*/
	}
	button:hover{
		background-color: #ff2c2c;
	}
</style>