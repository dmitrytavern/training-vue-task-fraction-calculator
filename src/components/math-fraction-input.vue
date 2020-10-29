<template>
	<input
			class="math__fraction-input"
			:class="{'is-error': hasError}"
			type="number"
			:style="styles"
			:value="modelValue"
			@input="update($event)"
	>
</template>

<script lang="ts">
import {defineComponent, ref, computed, watch, toRefs } from 'vue'

export default defineComponent({
	name: "math-fraction",
	props: {
		modelValue: {
			type: Number,
			default: 0,
		},
	},
	setup(props, { emit }) {
		const { modelValue } = toRefs(props)
		const hasError = ref(false)

		const update = ($event: InputEvent) => {
			emit('update:modelValue', +($event.target as HTMLInputElement).value)
		}

		const styles = computed(() => {
			const val = modelValue.value.toString().length
			return { width: val+1+'em' }
		})

		watch(modelValue, (newVal) => {
			hasError.value = isNaN(newVal)
		})

		return {
			update,
			styles,
			hasError,
			modelValue,
		}
	},
})
</script>

<style scoped>
.math__fraction-input {
	border: none;
	outline: none;
	background: none;
	height: 30px;
	padding: 5px;
	-moz-appearance: textfield;
	text-align: center;
}

.math__fraction-input.is-error {
	color: #6d1212;
}
</style>