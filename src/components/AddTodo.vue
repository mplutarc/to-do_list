<template>
	<div class="form">
		<form @submit="addTodo">
			<input type="text" v-model="title" name="title" required>
			<button type="submit">+</button>
		</form>
	</div>
</template>
<script>
import * as uuid from 'uuid';
export default {
	name: 'AddTodo',
	data() {
		return {
			title: ''
		}
	},
	methods: {
		addTodo(e) {
			e.preventDefault();
			const newTodoObj = {
				id: uuid.v4(),
				title: this.title,
				completed: false
			};
			this.$emit('add-todo', newTodoObj);
			this.title = '';
		}
	}
}
</script>
<style scoped>
.form{
	width: 100%;
	max-width: 335px;
}
form{
	margin: 0;
	display: flex;
	justify-content: space-between;
}
input{
	border-radius: 5px;
	border: none;
	margin-right: 1em;
	width: 87%;
}
input:focus{
	outline: none;
}
button{
	border: none;
	background-color: rgb(84 220 109);
	border-radius: 5px;
	height: 21px;
}
button:hover{
	background-color: rgb(138, 238, 76);
}
@media (min-width: 375px){
	.form{
		width: 60%;
	}
	/*form{*/
	/*}*/
}
</style>