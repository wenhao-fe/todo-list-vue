<template>
	<div id="create-todo">
		<input type="text " placeholder="请输入待办事项" id="new-todo" v-model="val" @keydown="inputTodos($event)" />
	</div>
</template>

<script>
import { Bus } from "@/event-bus";
export default {
	name: "create-todo",
	data() {
		return {
			val: "",
		};
	},
	methods: {
		inputTodos(e) {
			if (e.keyCode === 13) {
				if (!this.val.trim()) {
					alert("请输入待办事项！");
					return;
				}
				Bus.$emit("addTodos", this.val);
				this.val = "";
			}
		},
	},
};
</script>

<style></style>
