<script lang="ts">
	import { answerOptions, type answerOption } from "../types/answerOption";

  let options = answerOptions;
  export let onSelect: (a:answerOption) => void;

</script>

<div class="option-root">
  <ul>
  {#each options as opt}
    <li>
      <button on:click={() => onSelect(opt)}>{opt}</button>
    </li>
  {/each}
  </ul>
</div>

<style>
  .option-root{
    background-color: darkslategray;
    width: 100%;
    height: 100%;
  }
  ul {
    list-style: none;
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-template-rows: 1fr 1fr;
    padding: 0;
    margin: 0;
    width: 100%;
    height: 100%;
  }
  li{
    font-size: 1rem;
  }
  button{
    background: rgba(255, 255, 255, 0.064);
    width: 100%;
    height: 100%;
    border: 1px solid rgba(255, 255, 255, 0.264);
    border-radius: 0.25rem;
  }
  button:hover{
    background: rgba(255, 255, 255, 0.164);
  }
</style>