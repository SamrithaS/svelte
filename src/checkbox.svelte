<script>
	import Button from './button.svelte';
    export let tasks;
    export let deleteItem;
</script>

<style>
    div{
        display:flex;
        justify-content:space-between;
        align-items:center;
    }
    div.flex{
        max-width: 220px;
        margin: 0 auto;
    }
    input{
        margin:0 8px 0 0;
    }
    input:checked+p{
        opacity:40%;
    }
</style>

{#each tasks as task}
    <div class="flex">
        <div>
            <input type="checkbox" bind:checked={task.check}/>
            <p>{task.name}</p> 
        </div>
   
    <Button text="clear" handleClick={()=>deleteItem(task.name)}/>
    </div>
{/each}
