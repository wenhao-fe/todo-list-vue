<template>
	<ul id="todo-list">
		<list v-for="item in data" :key="item.id" :listData="item" />
	</ul>
</template>

<script>
import List from "./List";
export default {
	name: "todo-list",
	props: {
		data: Array,
	},
	components: {
		List,
	},
};
</script>

<style></style>
