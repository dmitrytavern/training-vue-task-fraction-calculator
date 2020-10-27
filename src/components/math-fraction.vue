<template>

	<div class="math__fraction">
		<div class="math__fraction-wrapper">
			<input type="number" v-model.number="fraction.numerator">
			<span></span>
			<input type="number" v-model.number="fraction.denominator">
		</div>

		<button class="btn btn-remove" @click="remove" v-if="canRemove">-</button>
	</div>

</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
	name: "math-fraction",
	props: {
		fraction: Object,
		index: Number,
		canRemove: Boolean,
	},
	methods: {
		remove() {
			this.$emit('remove', this.index)
		},
	}
})
</script>

<style scoped>
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
</style>