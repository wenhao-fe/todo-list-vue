<template>
	<div id="todo-stats">
		<span class="todo-count">
			<span class="number">{{ data.filter(item => !item.done).length }}</span>
			<span class="word">项未完成</span>
		</span>
		<div v-if="data.filter(item => item.done).length !== 0">
			<span class="todo-clear">
				<a href="javascript:;" @click="removeDone">
					删除
					<span class="number-done">{{ data.filter(item => item.done).length }}</span>
					项已完成
					<span class="word-done">事项</span>
				</a>
			</span>
		</div>
	</div>
</template>

<script>
import { Bus } from "@/event-bus";

export default {
	name: "todo-stats",
	props: {
		data: Array,
	},
	methods: {
		removeDone() {
			Bus.$emit("removeDone");
		},
	},
};
</script>

<style></style>
