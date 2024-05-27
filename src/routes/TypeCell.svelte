<script lang="ts">
  import data from '$lib/typeData.json'
	import type { answerOption } from '../types/answerOption';
	import type { Type } from '../types/types';
	import OptionsMenu from './OptionsMenu.svelte';
  export let attacker: Type;
  export let defender: Type;

  let correctAnswer = data[attacker][defender] as answerOption;
  let myAnswer: "?" | answerOption = '?';
  let isAnswered = false;

  let isOpen = false;

  const trigger = (a: MouseEvent) => {
    isOpen = !isOpen;
  }

  const setAnswer = (a:answerOption) => {
    //isOpen = false;
    myAnswer = a;
    isAnswered = true;
  }
</script>

<button class={`base-cell ${myAnswer === correctAnswer ? 'correct' : ''}`} on:click={trigger}>

  {#if isOpen}
    <OptionsMenu onSelect={setAnswer} />
  {:else}
  {myAnswer}
  {/if}
</button>

<style>
  .base-cell{
    background-color: rgb(10, 77, 43);
    border-radius: .5rem;
    border: 1px solid black;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 2rem;
    color: black
  }
  .base-cell:hover{
    background-color:rgba(10, 77, 40, 0.5);
  }
  .correct{
    background-color:rgba(6, 136, 34, 0.604);
  }
</style>
