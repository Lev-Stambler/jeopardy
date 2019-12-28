<!-- {question} -->
<style>
  .countdown {
    position: absolute;
    top: 10px;
    right: 10px;
  }
</style>
<div class="blue-container" in:fade>
  <div class="question statement">
    {question}
  </div>
  <button class="button-show" on:click={() => window.location.hash = `#/answer/${params.category}/${params.number}`}>
    <div>See Answer</div>
  </button>
  <div class="countdown">
    <Countdown time=33 />
  </div>
</div>
 <audio controls autoplay="autoplay" style="display: none;">  
    <source src="/static/Jeopardy-theme-song.mp3" type="audio/ogg">  
    <source src="/static/Jeopardy-theme-song.mp3" type="audio/mpeg">  
  </audio>
<script>
  import Countdown from '../general/Countdown.svelte' 
	import { fade } from 'svelte/transition';
  export let params = {}
  import { getContext, setContext } from 'svelte'
  let question = getContext('questions')[params.category][params.number]
  setTimeout(() => window.location.hash = `#/answer/${params.category}/${params.number}`, 33000)

</script>