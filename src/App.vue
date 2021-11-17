<template>
	<div id="app">
		<h1>Tarefas</h1>
		<form class="addTaskContainer" >
			<input type="text" placeholder="Tarefa" v-model="inputTask"> 
			<input type="text" placeholder="Descrição" v-model="inputDescription"> 

			<select name="inputTasks" id="inputTasks" v-model="inputPriority">
				<option value="">Escolha a prioridade</option>
				<option value="high">Alta prioridade</option>
				<option value="medium">Média Prioridade</option>
				<option value="low">Baixa Prioridade</option>
			</select>
			<button @click.prevent="addTask"> + </button>
		</form>

		<div class="taskContainer">
			<TaskCard 
				@delete="deleteTask(task.id)"
				@complete="completeTask(task.id)"
				v-for="task in tasks" 
				:key="task.id" 
				:title="task.title"  
				:description="task.description" 
				:priority="task.priority"
			/>
		</div>
		<div class="completedTasksContainer">
		
			<div style="width: 100%; display: flex;  justify-content: space-between">
				<h3>Tarefas concluídas</h3>
				<button class="clearTasks" @click="clearCompletedTasksList">
					limpar tarefas concluídas
				</button>
			</div>
			<CompletedTaskCard 
				v-for="task in completedTasksList" 
				:key="task.id" 
				:title="task.title"  
				:description="task.description" 
				:priority="task.priority"
			/>
		</div>
	</div>
</template>

<script>
	import TaskCard from './components/TaskCard.vue'
	import CompletedTaskCard from './components/CompletedTaskCard.vue'

	export default {
		components: {
			TaskCard, 
			CompletedTaskCard
		},

		data(){
			return {
				completedTasksList: [],
				currentTask: {},
				mensagem: '',
				inputTask: '',
				inputDescription: '', 
				inputPriority: '',
				taskItem: {},
				tasks: [	
					{	
						id: Math.random(),
						title: "Avaliação na academia", 
						description: " ABVC Qui anim Lorem deserunt eu.Incididunt tempor aute cillum nisi.",
						priority: "high"
					}, 
					{
						id: Math.random(),
						title: "Fazer feira saudável", 
						description: "Ipsum fugiat reprehenderit sunt ea nostrud veniam consectetur cillum reprehenderit excepteur pariatur.",
						priority: "medium"
					}
					
				] 
			
			}
		},

		methods: {
			addTask() {
				this.taskItem = {
						id: Math.random(),
						title: this.inputTask, 
						description: this.inputDescription,
						priority: this.inputPriority
				}

				console.log(this.taskItem)

				this.tasks.push(this.taskItem)

				this.inputTask = ''
				this.inputDescription = ''
				this.inputPriority = ''

			},
			deleteTask(id){
				let itemId = id
				console.log(itemId)

				let result = this.tasks.filter((task) => {
					return task.id !== itemId
				})
				this.tasks = result
				
			}, 
			completeTask(id){
				let itemId = id

				let currentTaskItem = this.tasks.filter((task) =>{
					return task.id === itemId
				})
				
				let item = currentTaskItem[0]
				this.completedTasksList.push(item)


				let result = this.tasks.filter((task) => {
					return task.id !== itemId
				})
				this.tasks = result
			}, 
			clearCompletedTasksList(){
				this.completedTasksList = ''
			}
		},
		
	}


/* 

barra de progresso
componentes do card 
-		-> iterar em um array de tarefas
[tarefa1, tarefa2, tarefa3]

para calcular a barra de progresso: 
- 	regra de 3 
- 	total length do array: 100%
-	tarefas concluida: x 

dados passados do componente app para:
-> progress bar 
-> cards de tarefas
*/


</script>

<style>

	*{
		box-sizing: border-box;
		padding: 0; 
		margin: 0;
	}

	body {
		font-family: 'Lato', sans-serif;
		background: 
			linear-gradient(to bottom right, 
							rgb(66, 6, 78), 
							rgb(8, 29, 37));
		color: #FFF;
		height: auto;
		min-height: 100vh; 
	}

	#app {
		display: flex;
		flex: 1;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		height: auto;
		min-height: 100vh; 
		padding-bottom: 3rem;
	
	}

	#app h1 {
		margin-bottom: 5px;
		font-weight: 900;
		font-size: 2.8rem;
		letter-spacing: -2px;
		
	}

	.taskContainer{
		display: flex;
		justify-content: space-between;
		width: 80%; 
		max-width: 1000px;
		flex-wrap: wrap;
	}

	input {
		background-color: rgba(240, 255, 240, 0.151);
		border: none; 
		border-radius: 3px;
		height: 20px;
		width: 100%;
		padding: 20px;
		box-shadow: 2px 2px 8px rgba(0, 0, 0, 0.233);
		outline: none;
		color: rgb(231, 231, 231);
		font-size: 16px;
		letter-spacing: 1px;
		margin-top: 10px;
	}

	.addTaskContainer{
		display: flex; 	
		width: 420px;
		flex-direction: column;	
		align-items: center;
		margin-top: 1rem;

	}

	.addTaskContainer > button{
		background-color: rgb(30, 187, 9);
		border: none; 
		border-radius: 3px;
		font-size: 20px;
		cursor: pointer;
		transition: .2s;
		width: 100%;
		margin-top: 10px;
		padding: 10px
	}

	.addTaskContainer > button:hover{
		background-color: rgb(30, 141, 15);
	}

	
    select{
        width: 100%;
        height: 45px;
        margin-top: 10px;
        outline: none;
        border: none; 
        border-radius: 3px;
    }

	.completedTasksContainer{
		width: 80%; 
		max-width: 1000px;
		display: flex;
		gap: 20px; 
		width: 80%;
		
		flex-wrap: wrap;
		margin-top: 120px;	
	}

	.completedTasksContainer h3 {
		font-size: 1.5rem;
		color: #fcfcfc;
		margin-top: 40px;
	}

	.clearTasks{
		background-color: brown;
		height: 25px;
		color: rgb(166, 169, 172); 
		border: none;
		padding: 0 20px; 
		border: none; 
		margin-top: 35px;
		border-radius: 10px;
		cursor: pointer;
		transition:.2s;
	}

	.clearTasks:hover{
		filter: brightness(0.8)
	}

</style>
