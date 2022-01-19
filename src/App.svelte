<script>
	import { FeedbackStore } from './stores/feddback';
	import Form from './components/UI/Form.component.svelte';
	import FeedbackList from './components/Data/FeedbackList.component.svelte';
	import FeedbackStatistics from './components/Data/FeedbackStatistics.component.svelte';
    import { onDestroy, onMount } from 'svelte';

	let feedbackList = [];
	
	onMount(() => {
		const unsebscribe = FeedbackStore.subscribe(data => { feedbackList = data; });
	});

	$: count = feedbackList.length;
	$: averageRate = (feedbackList.reduce((newVal, {rating}) => newVal + rating, 0) / feedbackList.length);

	const deleteFeedback = (e) => {
		const feedbackItemId = e.detail;
		feedbackList = feedbackList.filter(item => item.id !== feedbackItemId);
	};

	const handleNewFeedback = (e) => {
		const newFeedback = e.detail;
		feedbackList = [newFeedback, ...feedbackList];
	};

	onDestroy(() => {
		unsebscribe();
	});
</script>

<main class="container">
	<Form on:new-feedback="{handleNewFeedback}" />
	<FeedbackStatistics {count} {averageRate} />
	<FeedbackList {feedbackList} on:delete-feedback="{deleteFeedback}" />
</main>