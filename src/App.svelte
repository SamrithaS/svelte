<script>
	import Checkbox from './checkbox.svelte';
	import Button from './button.svelte';
	import Input from './input.svelte'
	import { fly, fade } from 'svelte/transition';
	import { slide } from 'svelte/transition';
	import { crossfade } from 'svelte/transition';
	import { flip } from 'svelte/animate';
	import { quintOut } from 'svelte/easing';


	let value="",placeholder="add a task"
    let id=1;
	let tasks=[{
		check:false, name:"drink water", id:id++
		},
		{
		check:false, name:"meditate", id:id++
		}
	]
	const [send, receive] = crossfade({
		duration: d => Math.sqrt(d * 200),

		fallback(node, params) {
			const style = getComputedStyle(node);
			console.log(style.transform)
			const transform = style.transform === 'none' ? '' : style.transform;
			return {
				duration: 600,
				easing: quintOut,
				css: t => `
					transform: ${transform} scale(${t});;
					opacity: ${t}
				`
			};
		}
	});

    function Add (){
		if(value!=""){
		tasks = [...tasks, {check:false, name:value, id:id++}]
		value=""
		}
	}
	
	function deleteItem (val){
		tasks=tasks.filter((item)=>item.name!==val)
	}

	$: remaining = tasks.filter(t => !t.check).length;
</script>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
		
	}
	body{
		background-color:#ddbea9
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
	div.flex-x{
		font-size:20px;
		color:#bc6c25;
    	display:flex;
    	justify-content:space-between;
        align-items:center;
		margin:10px 10px;
	}
	div.flex{
		display:flex;
		justify-content:space-between;
		max-width: 240px;
		margin: 20px auto;
		padding:10px;
		border-radius:10px;
		background-color:#faedcd;
	}
	input{
    	margin:0 8px 0 0;
	}
	input:checked+label{
    	opacity:40%;
	}
	p{
		margin:0 auto;
		max-width: 280px;
		text-align:center;
		font-size:24px;
		color:#283618;
		font-weight:bold;
		padding:0;
	}
	label{
		word-wrap:normal
	}
	div.flex-center{
		display:flex;
		justify-content:center;
	}
	progress{
		margin-bottom:40px;
		width:220px;
		padding:10px;
	}
</style>

<main>
<div class="">
{#if remaining==0 }
	<p> All tasks are complete!!!!</p>
	{:else if remaining==1}
	<p>{remaining} task to complete! </p>
	{:else}
	<p>{remaining} tasks to complete! </p>
	{/if}
	<progress id="file" value={tasks.filter(i=>i.check).length} max={tasks.length}> 32% </progress>
	</div>

	<Input bind:value={value} {placeholder} {Add}/>
	<Button handleClick={Add} text="Add"/>
	{#each tasks as task (task.id)}
		<div class="flex" in:receive="{{key: task.id}}"
				out:send="{{key: task.id}}" animate:flip>
	  		<div class="flex-x">
				<input type="checkbox" bind:checked={task.check} id={task.id}/>
				<label for={task.id}>{task.name}</label> 
	 		 </div>
	
			<Button text="clear" handleClick={()=>deleteItem(task.name)}/>
		</div>
    {/each}

	
</main>