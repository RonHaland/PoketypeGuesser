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

  /** @type {HTMLButtonElement} */
	let buttonElement: HTMLButtonElement;

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

  const handleBlur = ({currentTarget, relatedTarget }: {currentTarget: any, relatedTarget:any }) =>{
    if (currentTarget.contains(relatedTarget)) return;
    isOpen = false;
  }
  const handleChildBlur = ({currentTarget, relatedTarget }: {currentTarget: any, relatedTarget:any }) =>{
    if (buttonElement.contains(relatedTarget)) return;
    isOpen = false;
  }
</script>

<button class={`base-cell 
  ${myAnswer === correctAnswer ? 'correct' : ''} 
  ${myAnswer !== '?' ? answerColors[myAnswer] : ''}
  ${isOpen ? 'flipped' : ''}`} 
  on:click={trigger}
  on:blur={handleBlur}
  bind:this={buttonElement}>

  {#if isOpen}
    <OptionsMenu onSelect={setAnswer} handleChildBlur={handleChildBlur} />
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
    width: 4.5rem;
    height: 4.5rem;
    padding:0.125rem;
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
  .base-cell:focus{
    outline: 2px solid white;
  }
  .base-cell.flipped{
    background-color: rgb(65, 65, 65);
    scale: -1.1 1.1;
  }
  .flipped:hover{
    scale: -1.1 1.1;
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
