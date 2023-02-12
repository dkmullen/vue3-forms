<template>
	<label v-if="label">{{ label }}</label>
	<!-- $attrs allows us to inject attributes into this component.
  ie, the type binding from the parent, our css classes, etc
  -->
	<input
		v-bind="$attrs"
		:value="modelValue"
		:placeholder="label"
		@input="$emit('update:modelValue', $event.target.value)"
		class="field"
	/>
</template>

<script>
export default {
	props: {
		label: {
			type: String,
			default: '',
		},
		// modelValue is expected in Vue 3 to be on a v-model - capable component
		modelValue: {
			type: [String, Number],
			default: '',
		},
	},
};
</script>
