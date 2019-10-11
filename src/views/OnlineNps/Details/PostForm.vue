<template>
	<div>
		<el-form
			ref="form"
			label-width="100px"
			:model="formData"
			:rules="formRules">
			<form-item label="你好" prop="name" flow-text="haha">
				<el-input placeholder="haha" v-model="formData.name"></el-input>
			</form-item>
			<form-item prop="age" flow-text="HEHE">
				<span slot="label">你妹的</span>
				<el-input placeholder="HEHE" v-model="formData.age"></el-input>
			</form-item>
		</el-form>
		<el-button @click="onClick">validate</el-button>
	</div>
</template>

<script>
	const FormItem = {
		props: {
			flowText: String
		},
		inject: ['flow'],
		render(h) {
			const props = this.$attrs
			const slots = Object.assign({}, this.$slots)
			if (this.flow) {
				slots.default = [h('div', {slot: 'default'}, this.flowText)]
			}
			const children = Object.keys(slots).map(slot => {
				return h('template', {slot}, slots[slot])
			})
			return h('el-form-item', {props}, children)
		}
	}

	export default {
		name: "OnlineNpsPostForm",
		components: {FormItem},
		props: {
			flow: {
				type: Boolean,
				default: false
			}
		},
		provide() {
			return {
				flow: this.flow
			}
		},
		data() {
			return {
				formData: {
					name: '',
					age: ''
				},
				formRules: {
					name: [{required: true, message: '请输入name', trigger: 'blur'}],
					age: [{required: true, message: '请输入age', trigger: 'blur'}]
				}
			}
		},
		methods: {
			onClick() {
				this.validate().then(() => {}).catch(() => {})
			},
			validate() {
				return new Promise((resolve, reject) => {
					this.$refs.form.validate((flag, result) => {
						console.log('flag: ', flag)
						console.log('result: ', result)
						if(flag) {
							return resolve()
						}
						const reason = Object.keys(result).map(key => result[key])[0][0]
						console.log('reason: ', reason)
						reject(reason)
					})
				})
			}
		}
	}
</script>

<style lang="scss" scoped>

</style>
