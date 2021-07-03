<template>
	<div id="app">
		<h2>My todolist</h2>
		<div class="instruments">
			<AddTodo v-on:add-todo="addTodo"/>
			<button v-on:click="deleteTodos" class="delete_all">Delete all</button>
		</div>
		<Todos v-bind:todos="todos" v-on:delete-todo="deleteTodo" v-on:completed-todo="markComplete"/>
	</div>
</template>
<script>
import Todos from "@/components/Todos";
import AddTodo from "@/components/AddTodo";

export default {
	name: 'app',
	components: {Todos, AddTodo},
	data() {
		return {
			todos: [
				{
					id: 1,
					title: 'Add your todo',
					completed: false
				},
			],
		}
	},
	methods: {
		addTodo(newTodoObj) {
			this.todos.unshift(newTodoObj)
			localStorage.setItem('todo_list', JSON.stringify(this.todos));
		},
		deleteTodo(todoId) {
			this.todos = this.todos.filter(todo => todo.id !== todoId)
			localStorage.setItem('todo_list', JSON.stringify(this.todos));
		},
		deleteTodos() {
			const deleteAll = confirm("Are you sure? All todos will be deleted");
			if (deleteAll){
				this.todos = [];
			}
			localStorage.setItem('todo_list', JSON.stringify(this.todos));
		},
		markComplete(completedTodo){
			const completed = this.todos.find(todo => todo.id === completedTodo.id);
			this.deleteTodo(completed.id)
			let start = this.todos.findIndex(el => el.completed === true)
			if(completed.completed === false && start !== -1) {
				this.todos.splice(start, 0, completed);
			}
			else{
				this.todos = [...this.todos, completed];
			}
			localStorage.setItem('todo_list', JSON.stringify(this.todos));
		},
		getTodos() {
			if (localStorage.getItem('todo_list')) {
				this.todos = JSON.parse(localStorage.getItem('todo_list'));
			}
		},
	},
	mounted() {
		this.getTodos();
	},
}
</script>
<style>
@font-face{
	font-family: Jura;
	src: url(assets/20783.ttf);
}
*{
	font-family: Jura, serif;
	font-size: 16px;
	font-weight: 600;
	line-height: 1rem;
}
h2{
	font-size: 32px;
}
body{
	margin: 0;
	background: linear-gradient(131deg, rgba(217,26,212,1) 0%, rgba(201,244,111,1) 47%, rgba(254,255,0,0.9500175070028011) 100%) no-repeat;
}
#app{
	width: 90%;
	margin: 30px auto;
}
button{
	transition: all 1s ease-in-out;
}
button:hover{
	transition: all 0.2s ease-in-out;
}
.instruments{
	display: flex;
	height: 60px;
	flex-direction: column-reverse;
	justify-content: space-between;
	align-items: flex-end;
}
.delete_all{
	border: none;
	background-color: #fc5e5e;
	border-radius: 5px;
	height: 25px;
}
.delete_all:hover{
	background-color: #ff2c2c;
}
@media (min-width: 375px) {
	.instruments{
		align-items: center;
		flex-direction: row;
		justify-content: space-between;
		margin-bottom: 1em;
		padding-right: 1em;
	}
}
@media (min-width: 768px) {
	#app{
		width: 500px;
	}
}
</style>