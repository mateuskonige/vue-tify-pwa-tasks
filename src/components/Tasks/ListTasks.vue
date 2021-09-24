<template>
	<v-container>
		<h2 class="text-center">{{ title }}</h2>

		<form action="">
			<v-row>
				<v-col>
					<v-text-field
						label="Nova tarefa"
						:append-icon="inputNewTask.name ? 'mdi-send' : ''"
						@click:append.prevent="onSubmit"
						v-model="inputNewTask.name"
					></v-text-field>
				</v-col>
			</v-row>
		</form>

		<v-alert v-if="tasks == ''" dense text type="success">
			A lista de tarefas está limpa.
		</v-alert>

		<v-simple-table v-else>
			<thead>
				<tr>
					<th class="text-left">
						#
					</th>
					<th class="text-left">
						Tarefa
					</th>
					<th class="text-left">
						Ações
					</th>
				</tr>
			</thead>
			<tbody>
				<tr v-for="(task, index) in tasks" :key="index">
					<td>{{ index }}</td>
					<td>{{ task.name }}</td>
					<td>
						<v-menu transition="slide-x-transition" bottom right>
							<template v-slot:activator="{ on, attrs }">
								<v-btn icon v-bind="attrs" v-on="on">
									<v-icon>mdi-dots-vertical</v-icon>
								</v-btn>
							</template>

							<v-list>
								<v-list-item>
									<v-btn
										text
										@click.prevent="editTask(index)"
									>
										Editar
									</v-btn>
								</v-list-item>
								<v-list-item>
									<v-btn text color="error"
									@click.prevent="deleteTask(index)">
										Excluir
									</v-btn>
								</v-list-item>
							</v-list>
						</v-menu>
					</td>
				</tr>
			</tbody>
		</v-simple-table>
	</v-container>
</template>

<script>
export default {
	data() {
		return {
			title: "Lista de tarefas",
			tasks: [],
			inputNewTask: {
				id: "",
				name: "",
			},
			updating: false,
			updatedId: '',
		};
	},
	methods: {
		onSubmit() {
			if (this.updating) {
				this.updateTask();
				return;
			}
			this.saveTask();
		},
		saveTask() {
			this.inputNewTask.id = this.tasks.length + 1;
			this.tasks.unshift(this.inputNewTask);
			this.inputNewTask = {};
		},
		editTask(id) {
			this.inputNewTask = this.tasks[id];
			this.updatedId = id;
			this.updating = true;
		},
		updateTask(){
			this.tasks[this.updatedId] = this.inputNewTask
			this.inputNewTask = {};
			this.updating = false;
		},
		deleteTask(id) {
			this.tasks.splice(id, 1)
		}
	},
};
</script>

<style></style>
