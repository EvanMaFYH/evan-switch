<template>
	<view class="evan-switch-show">
		<view class="evan-switch-show__title">
			<text class="evan-switch-show__title__item">基础用法</text>
		</view>
		<evan-switch @change="onChagne" v-model="checked"></evan-switch>
		<view class="evan-switch-show__title">
			<text class="evan-switch-show__title__item">禁用</text>
		</view>
		<evan-switch :disabled="true" v-model="checked"></evan-switch>
		<view class="evan-switch-show__title">
			<text class="evan-switch-show__title__item">自定义颜色</text>
		</view>
		<evan-switch v-model="checked" activeColor="#00a231" inactiveColor="red"></evan-switch>
		<view class="evan-switch-show__title">
			<text class="evan-switch-show__title__item">自定义大小</text>
		</view>
		<evan-switch v-model="checked" :size="20"></evan-switch>
		<view class="evan-switch-show__title">
			<text class="evan-switch-show__title__item">自定义value值（当前选中的值：{{customChecked}}）</text>
		</view>
		<evan-switch v-model="customChecked" activeValue="value1" inactiveValue="value2"></evan-switch>
		<view class="evan-switch-show__title">
			<text class="evan-switch-show__title__item">拦截状态变更</text>
		</view>
		<evan-switch v-model="checked" :beforeChange="beforeChange"></evan-switch>
		<view class="evan-switch-show__title">
			<text class="evan-switch-show__title__item">拦截状态变更Promise</text>
		</view>
		<evan-switch v-model="checked" :beforeChange="beforeChangePromise"></evan-switch>

		<view class="evan-switch-show__title">
			<text class="evan-switch-show__title__item">循环switch，第二个拦截</text>
		</view>
		<block v-for="(item,index) in switchList" :key="index">
			<evan-switch v-model="item.value" :extraData="index" :beforeChange="beforeListChange"></evan-switch>
		</block>
		<!-- #ifdef APP-PLUS -->
		<button @click="goNvue">nvue页面</button>
		<!-- #endif -->
	</view>
</template>

<script>
	import EvanSwitch from '@/components/evan-switch/evan-switch.vue'
	export default {
		components: {
			EvanSwitch
		},
		data() {
			return {
				checked: true,
				customChecked: 'value1',
				switchList: [{
						value: true
					},
					{
						value: false
					},
					{
						value: false
					},
					{
						value: false
					},
					{
						value: true
					},
				]
			}
		},
		onLoad() {

		},
		methods: {
			beforeChange(e) {
				uni.showToast({
					title: '开关切换被拦截'
				})
				return false
			},
			beforeChangePromise(e) {
				return new Promise((resolve, reject) => {
					uni.showModal({
						title: '提示',
						content: `你确定要${e?'打开':'关闭'}吗`,
						success: (res) => {
							if (res.confirm) {
								resolve()
							} else if (res.cancel) {
								reject()
							}
						}
					})
				})
			},
			beforeListChange(e, extraData) {
				if (extraData === 1) {
					return false
				}
				return true
			},
			onChagne(e) {
				console.log(e)
			},
			goNvue(nv) {
				uni.navigateTo({
					url: '/pages/app/app'
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
	.evan-switch-show {
		padding: 20px;

		&__title {
			padding: 10px 0;

			&__item {
				font-size: 16px;
				color: #333;
				font-weight: bold;
			}
		}
	}
</style>
