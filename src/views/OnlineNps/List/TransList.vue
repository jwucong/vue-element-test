<template>
	<base-list
		v-bind="$attrs"
		v-on="$listeners">
		<template slot="expand" slot-scope="{row}">
			<div>ID: {{row.id}}</div>
			<div>name: {{row.name}}</div>
			<div>age: {{row.age}}</div>
			<div>aiHao: {{row.aiHao}}</div>
		</template>
		<el-table-column label="ID" prop="id"></el-table-column>
		<el-table-column label="name" prop="name"></el-table-column>
		<el-table-column label="age" prop="age"></el-table-column>
		<el-table-column label="aiHao" prop="aiHao"></el-table-column>
	</base-list>
</template>

<script>
	import BaseList from './BaseList'

	export default {
		name: "OnlineNpsTransList",
		components: {BaseList},
	}
</script>

<style lang="scss" scoped>

</style>
