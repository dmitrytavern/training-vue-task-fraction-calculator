<template>
	<div class="app">
		<h1>Calc Fractions App</h1>
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

h1 {
	font-size: 24px;
}

.app {
	display: flex;
	justify-content: center;
	flex-direction: column;
	padding-top: 180px;
}

.container {
	margin-top: 30px;
}

.btn {
	border-radius: 4px;
	cursor: pointer;
	border: none;
	outline: none;
	background: none;
}
</style>
