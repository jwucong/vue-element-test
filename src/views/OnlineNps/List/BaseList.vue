<template>
	<el-table
		ref="table"
		v-loading="loading"
		:data="tableData"
		@selection-change="handleSelectionChange"
		style="width: 100%">
		<el-table-column type="expand">
			<slot name="expand" slot-scope="scope" v-bind="scope"></slot>
		</el-table-column>
		<el-table-column type="selection" width="50"></el-table-column>
		<slot></slot>
		<el-table-column label="操作" width="150" align="center">
			<template slot-scope="{row}">
				<a href="javascript:;" class="handle-btn">详情</a>
				<a href="javascript:;" class="handle-btn" @click="emitApproval(row)">审批</a>
			</template>
		</el-table-column>
	</el-table>
</template>

<script>
	export default {
		name: "OnlineNpsOrderList",
		props: {
			data: {
				type: Array,
				default: () => ([])
			},
			loading: {
				type: Boolean,
				default: false
			},
			selection: {
				type: Array,
				default: () => ([])
			}
		},
		data() {
			return {

			}
		},
		computed: {
			tableData() {
				const list = this.data
				return Array.isArray(list) ? list : []
			},
			multipleSelection: {
				get() {
					return this.selection
				},
				set(value) {
					this.$emit('update:selection', this.copy(value))
				}
			}
		},
		methods: {
			copy(value) {
				return JSON.parse(JSON.stringify(value))
			},
			handleSelectionChange(selection) {
				this.multipleSelection = selection
			},
			clearSelection() {
				this.$refs.table.clearSelection()
			},
			emitApproval(order) {
				this.$emit('approval', this.copy(order))
			}
		}
	}
</script>

<style lang="scss" scoped>
	.handle-btn {
		display: inline-block;
		padding: 0 5px;
		margin-right: 5px;
		text-decoration: none;
		&:last-child {
			margin-right: 0;
		}
	}
</style>
