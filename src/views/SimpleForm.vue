<template>
	<div>
		<h1>Create an event</h1>
		<!-- Block the default submit and page reload, and instead use a custom method -->
		<form @submit.prevent="sendForm">
			<BaseSelect
				:options="categories"
				v-model="event.category"
				label="Select a category"
			/>

			<h3>Name & describe your event</h3>

			<BaseInput v-model="event.title" label="Title" type="text" />

			<BaseInput v-model="event.description" label="Description" type="text" />

			<h3>Where is your event?</h3>

			<BaseInput v-model="event.location" label="Location" type="text" />

			<h3>Are pets allowed?</h3>
			<div>
				<BaseRadioGroup
					v-model="event.pets"
					name="pets"
					:options="petOptions"
				/>
			</div>

			<h3>Extras</h3>
			<div>
				<BaseCheckbox v-model="event.extras.catering" label="Catering" />
			</div>

			<div>
				<BaseCheckbox v-model="event.extras.music" label="Live music" />
			</div>
			<!-- Don't use a click-listener on a form submit button as it gets in the way
      of the form element communicating with a screen reader. Likewise, specifing type="submit", 
      even though it is default, is good for screen readers. And DON'T disable the submit button!! -->
			<button type="submit">Submit</button>
		</form>

		<pre>{{ event }}</pre>
	</div>
</template>

<script>
import axios from 'axios';

export default {
	data() {
		return {
			categories: [
				'sustainability',
				'nature',
				'animal welfare',
				'housing',
				'education',
				'food',
				'community',
			],
			event: {
				category: '',
				title: '',
				description: '',
				location: '',
				pets: 1,
				extras: {
					catering: false,
					music: false,
				},
			},
			petOptions: [
				{ label: 'Yes', value: 1 },
				{ label: 'No', value: 0 },
			],
		};
	},
	methods: {
		sendForm(e) {
			axios
				.post(
					'https://my-json-server.typicode.com/Code-Pop/Vue-3-Forms/events',
					this.event
				)
				.then(function (response) {
					console.log('Response', response);
				})
				.catch(function (err) {
					console.log('Error', err);
				});
		},
	},
};
</script>
