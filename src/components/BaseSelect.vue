<template>
	<label v-if="label">{{ label }}</label>
	<!-- select elements fire a change event on select, so, unlike with
    the input, we have to listen for it and emit 
      We could use @change syntax here and bind the change event directly
    to the element, but instead we are combining it with attrs, so 
    @change becomes onChange -->
	<select
		class="field"
		:value="modelValue"
		v-bind="{
			...$attrs,
			onChange: ($event) => {
				$emit('update:modelValue', $event.target.value);
			},
		}"
	>
		<option
			v-for="option in options"
			:value="option"
			:key="option"
			:selected="option === modelValue"
		>
			{{ option }}
		</option>
	</select>
</template>

<script>
export default {
	props: {
		label: {
			type: String,
			default: '',
		},
		modelValue: {
			type: [String, Number],
			default: '',
		},
		options: {
			type: Array,
			required: true,
		},
	},
};
</script>
