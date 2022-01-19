<script>
    import { createEventDispatcher } from 'svelte';
    import Card from '../UI/Card.component.svelte';
    export let item = {};

    const dispatch = createEventDispatcher();
    const handleDelete = itemId => {
        dispatch('delete-feedback', itemId);
    };
</script>

<Card>
    <div class="rating">{item.rating}</div>
    <button type="button" class="delete" on:click="{() => handleDelete(item.id)}">X</button>
    <p class="text">{item.text}</p>
</Card>

<style>
    .rating {
        position: absolute;
        top: -10px;
        left: -10px;
        width: 50px;
        height: 50px;
        background: #ff6a95;
        color: #fff;
        border: 1px #eee solid;
        border-radius: 50%;
        padding: 10px;
        text-align: center;
        font-size: 19px;
    }
    .delete {
        position: absolute;
        top: 10px;
        right: 20px;
        cursor: pointer;
        background: none;
        border: none;
    }
</style>