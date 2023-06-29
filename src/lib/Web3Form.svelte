<script lang="ts">
	import type { EventHandler } from 'svelte/elements';

	interface Response<T> {
		success: boolean;
		message: string;
		data: T;
	}

	type OnResponse = <T extends {}>(message: string, data: Response<T>) => void;
	type HandleSubmit =
		| EventHandler<
				Event & {
					readonly submitter: HTMLElement | null;
				},
				HTMLFormElement
		  >
		| null
		| undefined;

	export let apikey: string;

	export let from_name = '';
	export let replyto = '';
	export let disableStatus = false;
	export let honeypot = true;
	export let inputClass = '';
	export let formClass = '';
	export let redirect = '';
	export let subject = '';
	export let status = '';

	export let onError: OnResponse = () => {};
	export let onSuccess: OnResponse = () => {};

	const handleSubmit: HandleSubmit = async <T extends {}>(form: {
		currentTarget: HTMLFormElement | undefined;
	}) => {
		status = 'Submitting...';
		const formData = new FormData(form.currentTarget);
		const object = Object.fromEntries(formData);
		const json = JSON.stringify({ apikey, ...object });

		const response = await fetch('https://api.web3forms.com/submit', {
			method: 'POST',
			headers: {
				'Content-Type': 'application/json'
			},
			body: json
		});

		const data: Response<T> = await response.json();
		status = data.message || 'Success';
		if (data.success === true) {
			onSuccess(data.message, data);
		} else {
			onError(data.message, data);
		}
	};
</script>

<form on:submit|preventDefault={handleSubmit} class="W3F__Form {formClass}">
	{#if honeypot}
		<input type="checkbox" name="botcheck" class="W3F__Honeypot" style="display: none;" />
	{/if}
	{#if subject !== ''}
		<input type="hidden" name="subject" value={subject} />
	{/if}
	{#if redirect !== ''}
		<input type="hidden" name="redirect" value={redirect} />
	{/if}
	{#if replyto !== ''}
		<input type="hidden" name="replyto" value={replyto} />
	{/if}
	{#if from_name !== ''}
		<input type="hidden" name="from_name" value={from_name} />
	{/if}
	{#if !$$slots.default}
		<input
			type="text"
			name="name"
			required
			placeholder="Name"
			class="W3F__Name W3F__Inputs {inputClass}"
		/>
		<input
			type="email"
			name="email"
			required
			placeholder="Email"
			class="W3F__Email W3F__Inputs {inputClass}"
		/>
		<textarea
			name="message"
			required
			rows="3"
			placeholder="Your message..."
			class="W3F__Message W3F__Inputs {inputClass}"
		/>
	{/if}
	<slot />
	<input class="W3F__Submit {inputClass}" type="submit" />
</form>
{#if !disableStatus}
	<div class="W3F__Status">{status}</div>
{/if}
