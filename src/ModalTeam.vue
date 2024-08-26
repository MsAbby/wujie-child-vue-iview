<template>
	<Modal v-model="visible" width="60">
		<div class="c-transfer" >
			<div class="c-transfer-left">
				<Table
					:columns="columnsLeft"
					:data="data"
					:height="200"
					style="border-radius: 10px;"
					@on-select="handelSelect"
				></Table>
				<div style="height: 40px; padding: 40px 0;">
					<Page :total="100" @on-change="pageChange"/>
				</div>
			</div>
			<div class="c-transfer-right">
				<Table
					:columns="columnsRight"
					:data="selectList"
					:height="200"
					style="border-radius: 10px;"
				>
					<template slot-scope="{ row, index }" slot="action">
						<Button type="error" size="small" @click="remove(row, index)">移除</Button>
					</template>
				</Table>
			</div>
		</div>
	</Modal>
</template>
<script>
export default {
	name: 'ModalTeam',
	data() {
		return {
			visible: false,
			columnsLeft: [
				{
					type: 'selection',
					width: 60,
					align: 'center'
				},
				{
					title: '车型组',
					key: 'name'
				},
			],
			columnsRight: [
				{
					title: '车型组',
					key: 'name'
				},
				{
					title: '操作',
					slot:'action'
				},
			],
			data: [
				{
					name: 'John Brown',
					code: '1',
					_checked: false,
					_disabled: false
				},
				{
					name: 'Jim Green',
					code: '12',
					_checked: false,
					_disabled: false
				},
				{
					name: 'Joe Black',
					code: '123',
					_checked: false,
					_disabled: false
				},
				{
					name: 'Jon Snow',
					code: '1234',
					_checked: false,
					_disabled: false
				}
			],
			selectList: [],
		}
	},
	methods: {
		init() {
			this.visible = true;
		},
		
		handelSelect(val, row) {
			this.data = this.data.map(item => {
				if (item.code === row.code) {
					item._disabled = true;
					item._checked = true
				}
				return item
			})
			if (this.selectList.length > 0) {
				this.selectList.unshift(row)
			} else {
				this.selectList = val
			}
		},

		// 移除，当前要删除
		remove(row, index) {
			this.selectList.splice(index, 1)
			this.data = this.data.map(item => {
				if(item.code === row.code) {
					item._disabled = false;
					item._checked = false;
				}
				return item
			})
		},

		pageChange(page) {
			if (page === 1) {
				this.data = [
				{
					name: 'John Brown',
					code: '1',
					_checked: false,
					_disabled: false
				},
				{
					name: 'Jim Green',
					code: '12',
					_checked: false,
					_disabled: false
				},
				{
					name: 'Joe Black',
					code: '123',
					_checked: false,
					_disabled: false
				},
				{
					name: 'Jon Snow',
					code: '1234',
					_checked: false,
					_disabled: false
				}
			]
			} else if (page === 2) {
				this.data = [
					{
						name: '王武',
						code: '14',
						_checked: false,
						_disabled: false
					},
					{
						name: '王武11',
						code: '144',
						_checked: false,
						_disabled: false
					},
					{
						name: '找刘',
						code: '125',
						_checked: false,
						_disabled: false
					},
					{
						name: '888888',
						code: '1236',
						_checked: false,
						_disabled: false
					},
					{
						name: '哈哈',
						code: '12347',
						_checked: false,
						_disabled: false
					}
				]
			} else if (page === 3) {
				this.data = [
					{
						name: '转账',
						code: '148',
						_checked: false,
						_disabled: false
					},
					{
						name: '温热我认为热污染',
						code: '1258',
						_checked: false,
						_disabled: false
					},
					{
						name: '巍峨温热温热我热污染',
						code: '12368',
						_checked: false,
						_disabled: false
					},
					{
						name: '3232款垃圾袋来得及',
						code: '123487',
						_checked: false,
						_disabled: false
					}
				]
			} else {
				this.data = [
				{
					name: 'John Brown',
					code: '1',
					_checked: false,
					_disabled: false
				},
				{
					name: 'Jim Green',
					code: '12',
					_checked: false,
					_disabled: false
				},
				{
					name: 'Joe Black',
					code: '123',
					_checked: false,
					_disabled: false
				},
				{
					name: 'Jon Snow',
					code: '1234',
					_checked: false,
					_disabled: false
				}
			]
			}

			const selectCode = this.selectList.map((item) => item.code)
			this.data = this.data.map(item => {
				if(selectCode.includes(item.code)) {
					item._disabled = true;
					item._checked = true;
				}
				return item
			})
		}
	}
}
</script>
<style scoped>
.c-transfer {
	position: relative;
	line-height: 1.5;
	width: 100%;
}
.c-transfer-left {
	display: inline-block;
	width: 45%;
	height: 210px;
	font-size: 14px;
	vertical-align: middle;
	position: relative;
	border: 1px solid #dcdee2;
	border-radius: 10px;
	margin-right: 20px;
}

.c-transfer-right {
	display: inline-block;
	width: 45%;
	height: 210px;
	font-size: 14px;
	vertical-align: middle;
	position: relative;
	border: 1px solid #dcdee2;
	border-radius: 10px;
	margin-right: 20px;
}
</style>