<svelte:head>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@picocss/pico@1/css/pico.min.css">
</svelte:head>

<script>
    let ToDo = [];
    let textInput = "";

    function addToDo() {
        ToDo = [...ToDo, {content: textInput, editing: false, checked: false}]
    }

    function editing(i, isditing) {
        ToDo[i].editing = isditing;
    }
function deleteToDo(i) {
    ToDo.splice(i, 1);
    ToDo = ToDo;
}
</script>

<div style="margin: 0 auto; padding: 20px; width: 700px;">
    <h2 style="text-align: center;">ToDo List</h2>
    <p>Enter your ToDo here</p>
    <div style="display: flex;">
        <input type="text" bind:value={textInput}>
        <button style="width: 200px;" on:click={addToDo}>Add</button>
    </div>
</div> 

{#each ToDo as ToDo, i}
<div style="display: flex; align-items: baseline; width: 700px; margin: 0 auto;">
    {#if ToDo.editing}
        <input type="text" bind:value={ToDo.content}>
    {:else}
    <input type="checkbox" bind:checked={ToDo.checked}>
    <h4 style="flex-grow: 1;">{ToDo.content}</h4>
    {/if}
    <div style="display: flex;">
        {#if ToDo.editing}
            <button on:click={() => editing(i, false)}>Save</button>
        {:else}    
            <button on:click={() => editing(i, true)}>Edit</button>
        {/if} 
        <button on:click={() => deleteToDo(i,)}>Delete</button>
    </div>
</div> 
{/each}