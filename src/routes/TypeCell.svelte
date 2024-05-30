<script lang="ts">
  import data from '$lib/typeData.json'
	import { answerColors, type answerOption } from '../types/answerOption';
	import type { Type } from '../types/types';
	import OptionsMenu from './OptionsMenu.svelte';
  export let attacker: Type;
  export let defender: Type;
  export let updateFunc: (col:Type, row:Type, result:boolean) => void;

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
    updateFunc(defender, attacker, myAnswer === correctAnswer);
  }
</script>

<button class={`base-cell 
  ${myAnswer === correctAnswer ? 'correct' : ''} 
  ${myAnswer !== '?' ? answerColors[myAnswer] : ''}
  ${isOpen ? 'flipped' : ''}`} 
  on:click={trigger}
  on:mouseleave={() => isOpen = false}>

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
    color: black;
    position: relative;
    transition: scale 0.18s ease-out;
  }
  .base-cell:hover{
    scale: 1.1;
  }
  .base-cell:hover::after{
    border-radius: .5rem;
    content:' ';
    display: block;
    inset:0;
    position: absolute;
    pointer-events: none;
    background: rgba(255, 255, 255, 0.18);
  }
  .flipped{
    scale: -1 1;
  }
  .flipped:hover{
    scale: -1.1 1.1;
  }
  .correct{
    background-color:rgba(6, 136, 34, 0.604);
  }
  .black{
    background-color: rgba(0, 0, 0, 1);
    color: #aaa;
  }
  .red{
    background-color: rgb(145, 7, 7);
  }
  .grey{
    background-color: rgba(104, 104, 104, 1);
  }
  .green{
    background-color: rgba(13, 118, 4, 1);
  }
</style>
