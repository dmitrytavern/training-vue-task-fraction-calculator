<template>
	<div class="app">
		<div class="container">
			<div class="math">

				<div class="math__fraction" v-for="(fraction, index) in fractions">
					<div class="math__fraction-wrapper">
						<input type="number" v-model.number="fraction.numerator">
						<span></span>
						<input type="number" v-model.number="fraction.denominator">
					</div>

					<button class="btn btn-remove" @click="removeFraction(index)" v-if="fractions.length > 2">-</button>
				</div>

				<div class="math__symbol">=</div>
				<div class="math__result">{{ math }}</div>

			</div>

			<button class="math__add" @click="addFraction">Add fraction</button>

		</div>
	</div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'App',
	data() {
  	return {
			fractions: [
				{
					numerator: 1,
					denominator: 2,
				},
				{
					numerator: 1,
					denominator: 2,
				},
			]
		}
	},
	computed: {
  	math(): number {
  		let val = 0
			this.fractions.forEach((fraction) => {
				const numerator = fraction.numerator || 0
				const denominator = fraction.denominator || 0
				const value = numerator / denominator

				if (!isNaN(value) && value !== Infinity) {
					val += value
				}
			})
  		return val
		}
	},
	methods: {
		addFraction() {
			this.fractions.push({
				numerator: 0,
				denominator: 0,
			})
		},

  	removeFraction(index: number) {
			this.fractions.splice(index, 1)
		},
	},
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

.math {
	display: flex;
	align-items: center;
	justify-content: center;
	margin-top: 30px;
}

.math__symbol,
.math__result {
	font-size: 22px;
	padding: 0 10px;
}

.math__add {
	margin-top: 15px;
}

.math__fraction {
	display: flex;
	flex-direction: column;
	align-items: center;
}

.math__fraction .math__fraction-wrapper {
	display: flex;
	flex-direction: column;
	align-items: center;
	padding: 0 10px;
	position: relative;
}
.math__fraction:not(:first-child) > .math__fraction-wrapper {
	padding-left: 20px;
}
.math__fraction:not(:first-child) > .math__fraction-wrapper:after {
	content: '+';
	position: absolute;
	top: 50%;
	left: 0;
	transform: translateY(-50%);
	font-size: 22px;
}

.math__fraction span {
	width: 50px;
	height: 2px;
	background: #000;
	margin: 5px 0;
}

input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
	-webkit-appearance: none;
	margin: 0;
}

.math__fraction input {
	width: 30px;
	height: 30px;
	padding: 5px;
	-moz-appearance: textfield;
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
