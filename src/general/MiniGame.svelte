<div class="cont">
    <div class="statement">
        Get ready to play {title}!
    </div>
    <div class="desc">
        {@html desc}
    </div>
    <div class="done">
        <button class="button-show" on:click={submit}>Go Home</button>
    </div>
</div>
<script>
    import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

	const submit = () => dispatch('submit');
    export let title = ""
    export let desc = "desc her"
</script>
<style>
.desc {
    font-size: 25px;
    max-width: 70%; 
}
.cont {
    flex-direction: column;
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    z-index: 1000;
    padding-bottom: 5rem;
    background: rgb(5, 5, 5);
    display: flex;
    align-items: center;
    justify-content: center;
}
</style>