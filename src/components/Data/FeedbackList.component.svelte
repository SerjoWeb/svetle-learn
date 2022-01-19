<script>
    import { fade, scale } from 'svelte/transition';
    import FeedbackItem from '../Data/FeedbackItem.component.svelte';
    export let feedbackList = [];
</script>

{#each feedbackList as feedBack (feedBack.id)}
    <div in:scale out:fade="{{ duration: 500 }}">
        <FeedbackItem item = {feedBack} on:delete-feedback />
    </div>
{/each}