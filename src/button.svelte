<script>
export let handleClick;
export let text;

</script>
<style>
    button.Clear{
        background-color:#283618;
        font-size:14px;
        color:white;
         padding: 10px 10px;
        margin:0;
    }
    button.Add{
        background-color:#d4a373;
        color:white;
        
        margin:0;
        padding: 10px 20px;
    }
    button{
        border-radius:15px;
        border:none
    }
   
</style>

<button class={`${text==="clear"?"Clear":"Add"}`} on:click={handleClick}>{text}</button>