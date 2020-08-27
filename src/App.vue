<template>
	<div id="todoapp">
		<TodoTitle />
		<div class="content">
			<Create />
			<div v-if="datas.length !== 0">
				<Todos :data="this.datas" />
				<State :data="this.datas" />
			</div>
		</div>
	</div>
</template>

<script>
import "./assets/index.css";
import { Bus } from "@/event-bus";
import TodoTitle from "./components/TodoTitle";
import Create from "./components/Create";
import Todos from "./components/Todos";
import State from "./components/State";

export default {
	name: "todoapp",
	components: {
		TodoTitle,
		Create,
		Todos,
		State,
	},
	data() {
		return {
			datas: [],
		};
	},
	mounted() {
		Bus.$on("addTodos", txt => {
			console.log(this.datas);
			this.datas.unshift({
				id: new Date().getTime(),
				txt,
				done: false,
			});
		});
		Bus.$on("changeDone", ({ id, done }) => {
			this.datas.map(item => {
				if (item.id === id) item.done = done;
			});
		});
		Bus.$on("remove", id => {
			this.datas = this.datas.filter(item => item.id !== id);
		});
		Bus.$on("editTxt", ({ id, txt }) => {
			this.datas.map(item => {
				if (item.id === id) item.txt = txt;
			});
		});
		Bus.$on("removeDone", () => {
			this.datas = this.datas.filter(item => !item.done);
		});
	},
	methods: {},
};
</script>

<style></style>
