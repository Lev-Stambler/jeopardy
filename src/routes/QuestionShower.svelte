<!-- {question} -->
<style>
  .answer-show div {
    color: white;
    font-size: 27px;
    text-decoration: none;
    font-weight: 600;
  }

  .answer-show {
    background: rgb(184, 184, 184);
    padding: 15px;
    border-radius: 10px;
    box-shadow: 0px 0px 10px 2px black;
    margin: 7px;
    margin-top: 2rem;
    cursor: pointer;
  }
</style>
<div class="container">
  <div class="question statement">
    {question}
  </div>
  <div class="img">
    <img src="https://images.pexels.com/photos/104827/cat-pet-animal-domestic-104827.jpeg?auto=compress&cs=tinysrgb&dpr=1&w=500" alt="">
  </div>
  <button class="answer-show" on:click={() => window.location.hash = `#/answer/${params.category}/${params.number}`}>
    <div>I give up</div>
  </button>
</div>
<script>
  export let params = {}
  import { getContext, setContext } from 'svelte'
  let question = getContext('questions')[params.category][params.number]
</script>