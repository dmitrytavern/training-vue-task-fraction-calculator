<template>
	<div class="app">
		<div class="container">
			<Math />
		</div>
	</div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import Math from '@/components/math.vue'

export default defineComponent({
  name: 'App',
	components: {
		Math
	}
});
</script>

<style>
* {
	box-sizing: border-box;
	margin: 0;
	padding: 0;
}

html,
body {
	height: 100%;
}

#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
	height: 100%;
}

.app {
	display: flex;
	justify-content: center;
	align-items: center;
	height: 100%;
}

.container {
	min-width: 360px;
	min-height: 250px;
	background: #f7f7f7;
}


.btn {
	width: 20px;
	height: 20px;
	border-radius: 4px;
	display: flex;
	align-items: center;
	justify-content: center;
	cursor: pointer;
	margin-top: 15px;
}

.btn-remove {
	color: #fff;
	background: #9e2929;
}
</style>
