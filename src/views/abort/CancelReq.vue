<template>
	<button @click="fn(1)">请求1</button>
	<button @click="fn(2)">请求2</button>
	<button @click="fn(3)">请求3</button>
	<button @click="abort">取消请求</button>
</template>

<script setup lang="ts">
import { request, abortReq } from '../../network/request'
import axios from 'axios'

const fn = (i) => {
	const req = [
		'http://127.0.0.1:9999/abort1',
		'http://127.0.0.1:9999/abort2',
		'http://127.0.0.1:9999/abort3'
	]
	const CancelToken = axios.CancelToken
	const source = CancelToken.source()
	request(
		{
			url: req[i - 1],
			method: 'get',
			// 这里记得小写
			cancelToken: source.token
			// params: {
			// 	t: Date.now()
			// }
		},
		source
	)

	// source.cancel() // 取消请求
}

const abort = () => abortReq()
</script>

<style lang="scss"></style>
