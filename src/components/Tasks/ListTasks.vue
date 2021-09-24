<template>
	<v-container>
		<h2 class="text-center">{{ title }}</h2>

		<form action="">
			<v-row>
				<v-col>
					<v-text-field
						label="Nova tarefa"
						:append-icon="inputNewTask.name ? 'mdi-send' : ''"
						@click:append="saveTask"
						v-model="inputNewTask.name"
					></v-text-field>
				</v-col>
			</v-row>
		</form>
		<v-simple-table>
			<thead>
				<tr>
					<th class="text-left">
						#
					</th>
					<th class="text-left">
						Nome
					</th>
					<th class="text-left">
						Ações
					</th>
				</tr>
			</thead>
			<tbody>
				<tr v-for="task in tasks" :key="task.id">
					<td>{{ task.id }}</td>
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
									<v-btn text>
										Editar
									</v-btn>
								</v-list-item>
								<v-list-item>
									<v-btn text color="error">
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
			tasks: [{ id: 1, name: "Lavar Louça" }],
			inputNewTask: {
				id: "",
				name: "",
			},
		};
	},
	methods: {
		saveTask() {
			this.inputNewTask.id = this.tasks.length + 1;
			this.tasks.unshift(this.inputNewTask);
			this.inputNewTask = {};
		},
	},
};
</script>

<style></style>
