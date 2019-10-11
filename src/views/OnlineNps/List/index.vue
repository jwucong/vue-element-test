<template>
	<div>
	<el-select v-model="listId" @change="handleListIdChange">
		<el-option label="Issue" value="issue-list"></el-option>
		<el-option label="Trans" value="trans-list"></el-option>
	</el-select>
	<component
		:is="listId"
		:data="orderList"
		:loading="loading"
		:selection.sync="selection"
		@approval="handleApproval">
	</component>
	</div>

</template>

<script>
	import IssueList from './IssueList'
	import TransList from './TransList'
	import {orderList} from '../mock/orderList'


	export default {
		name: "index",
		components: {
			IssueList,
			TransList
		},
		data() {
			return {
				listId: 'issue-list',
				orderList: orderList,
				loading: false,
				selection: []

			}
		},
		computed: {
		},
		mounted() {
			this.loading = true
			setTimeout(() => {
				this.loading = false
			}, 1000)
		},
		methods: {
			handleApproval(order) {
				console.log(order)
			},
			handleListIdChange() {
				this.selection = []
			}
		}
	}
</script>

<style lang="scss" scoped>

</style>
