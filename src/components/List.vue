<template>
	<li :class="edit ? 'editing' : ''">
		<div :class="`todo ${listData.done ? 'done' : ''}`">
			<div class="display">
				<input type="checkbox" class="check" :checked="listData.done" @click="changeDone(listData.id, $event)" />
				<div class="todo-content" @dblclick="editTodo">
					{{ listData.txt }}
				</div>
				<span class="todo-destroy" @click="remove(listData.id)"></span>
			</div>
		</div>
		<div class="edit">
			<input
				ref="getfocus"
				type="text"
				class="totdo-input"
				:value="val"
				@keyup="editTxt(listData.id, $event)"
				@blur="
					() => {
						this.edit = false;
					}
				"
			/>
		</div>
	</li>
</template>

<script>
import { Bus } from "@/event-bus";

export default {
	props: {
		listData: Object,
	},
	data() {
		return {
			edit: false,
			val: "",
		};
	},
	updated() {
		this.val = this.listData.txt;
		this.$refs.getfocus.focus();
	},
	methods: {
		editTxt(id, e) {
			if (e.keyCode === 13) {
				if (!e.target.value) {
					alert("请输入待办事项！");
					return;
				}
				Bus.$emit("editTxt", { id, txt: e.target.value });
				this.val = "";
				this.edit = false;
			}
		},
		changeDone(id, event) {
			Bus.$emit("changeDone", { id, done: event.target.checked });
		},
		remove(id) {
			Bus.$emit("remove", id);
		},
		editTodo() {
			this.edit = true;
		},
	},
};
</script>

<style></style>
