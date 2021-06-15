<script>
export let value=""
export let placeholder=""
export let Add;
 function handleKeyDown(e){
        if(e.key==="Enter"){
            Add()
        }
    }
</script>

<style>
    input{
        background-color:#283618;
        padding:10px 20px;
        border-radius:10px;
        color:white;
    }
    input:focus{
        border:none;
        outline:none;
    }
</style>
<input bind:value={value} {placeholder} on:keydown={handleKeyDown}/>
