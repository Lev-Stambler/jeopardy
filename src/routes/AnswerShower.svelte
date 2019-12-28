<div class="blue-container" in:fly={{y: 100}}>
  <div class="question statement">
    {answer}
  </div>
  <div class="img">
    <img src="https://images.pexels.com/photos/104827/cat-pet-animal-domestic-104827.jpeg?auto=compress&cs=tinysrgb&dpr=1&w=500" alt="">
  </div>
  <div>
    <button class="button-show" on:click="{correct}">
      <div>
        Correct
      </div>
    </button>
    <button class="button-show" on:click="{wrong}">
      <div>
        Wrong
      </div>
    </button>
  </div>
</div>
<script>
	import { fly } from 'svelte/transition';
  export let params = {}
  import { getContext, setContext } from 'svelte'
  function goHome() {
    window.location.hash = "#/"
  }
  function correct() {
    goHome()
  }
  function wrong() {
    goHome()
  }
  let answer = getContext('answers')[params.category][params.number]
</script>