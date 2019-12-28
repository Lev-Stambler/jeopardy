<!-- {question} -->
<style>
</style>
<div class="blue-container" in:fade>
  <div class="question statement">
    {question}
  </div>
  <div class="img">
    <img src="https://images.pexels.com/photos/104827/cat-pet-animal-domestic-104827.jpeg?auto=compress&cs=tinysrgb&dpr=1&w=500" alt="">
  </div>
  <button class="button-show" on:click={() => window.location.hash = `#/answer/${params.category}/${params.number}`}>
    <div>I give up</div>
  </button>
</div>
<script>
	import { fade } from 'svelte/transition';
  export let params = {}
  import { getContext, setContext } from 'svelte'
  let question = getContext('questions')[params.category][params.number]
</script>