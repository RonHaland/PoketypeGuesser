<script lang="ts">
	import { answerColors, answerOptions, type answerOption } from "../types/answerOption";

  let options = answerOptions;
  export let onSelect: (a:answerOption) => void;

</script>

<div class="option-root">
  <ul>
  {#each options as opt}
    <li>
      <button on:click={() => onSelect(opt)} class={answerColors[opt]}>{opt}</button>
    </li>
  {/each}
  </ul>
</div>

<style>
  .option-root{
    background-color: darkslategray;
    width: 100%;
    height: 100%;
    scale: -1 1;
  }
  ul {
    list-style: none;
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-template-rows: 1fr 1fr;
    gap: 1px;
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
    position: relative;
  }
  button:hover::after{
    content:' ';
    display: block;
    inset:0;
    position: absolute;
    background: rgba(255, 255, 255, 0.08);
  }
  .black{
    background-color: rgba(0, 0, 0, 0.667);
    color: #aaa;
  }
  .red{
    background-color: rgba(196, 17, 17, 0.139);
  }
  .grey{
    background-color: rgba(104, 104, 104, 0.22);
  }
  .green{
    background-color: rgba(13, 118, 4, 0.507);
  }
</style>