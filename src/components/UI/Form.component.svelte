<script>
    import { v4 as v4uuid } from 'uuid';
    import Card from './Card.component.svelte';
    import Button from './Button.component.svelte';
    import RatingSelection from './RatingSelection.component.svelte';
    import { createEventDispatcher } from 'svelte';

    let text = '';
    let btnDisabled = true;
    let minVal = 10;
    let warningMessage = null;
    let rating = 10;

    const dispatch = createEventDispatcher();

    const handleInput = () => {
        if (text.trim().length <= 10) {
            warningMessage = `Text must be at least ${minVal} characters`;
            btnDisabled = true;
        } else {
            warningMessage = null;
            btnDisabled = false;
        }
    };

    const handleRatingSelected = e => rating = e.detail;
    
    const handleSubmit = () => {
        if (text.trim().length > 10) {
            const newFeedback = {
                id: v4uuid(),
                text: text,
                rating: +rating
            };

            dispatch('new-feedback', newFeedback);

            text = '';
            rating = 10;
            btnDisabled = true;
        }
    };
</script>

<Card>
    <header>
        <h2>How would you rate your service with us?</h2>
    </header>

    <RatingSelection on:selected-rating="{handleRatingSelected}" />

    <form on:submit|preventDefault="{handleSubmit}">
        <div class="input-group">
            <input type="text" placeholder="Leave your feedback" bind:value="{text}" on:input="{handleInput}" />
            <Button type="submit" disabled="{btnDisabled}">Send</Button>
        </div>

        {#if warningMessage}
            <div class="warning-message">{warningMessage}</div>
        {/if}
    </form>
</Card>

<style>
    header {
        max-width: 400px;
        margin: auto;
    }

    header h2 {
        font-size: 22px;
        font-weight: 600;
        text-align: center;
    }

    .input-group {
        display: flex;
        flex-direction: row;
        border: 1px solid #ccc;
        padding: 8px 10px;
        border-radius: 8px;
        margin-top: 15px;
    }

    input {
        flex-grow: 2;
        border: none;
        font-size: 16px;
    }

    input:focus {
        outline: none;
    }

    .warning-message {
        padding-top: 10px;
        text-align: center;
        color: rebeccapurple;
    }
</style>