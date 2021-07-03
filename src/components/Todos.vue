<template>
	<div>
		<ul class="todo_list">
			<li v-bind:key="todo.id" v-for="todo in todos">
				<Todo v-bind:todo="todo" v-on:delete-todo="$emit('delete-todo', todo.id)" v-on:completed-todo="$emit('completed-todo', todo)"/>
			</li>
		</ul>
	</div>
</template>
<script>
import Todo from './Todo';
export default {
	name: 'Todos',
	components: {
		Todo,
	},
	props: [
		"todos"
	]
}
</script>
<style scoped>
	.todo_list{
		padding-inline-start: 0
	}
	li{
		list-style-type: none;
	}
</style>