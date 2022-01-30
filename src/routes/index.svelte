<script>
    let todos = [] ;
    let task = "";
    
    const addTodo = () => {
        let todo = {
            task: task,
            isComplete: false,
            createdAt: new Date(),
        }; 
        todos = [todo, ...todos]; //expand todo object and add the new one
        task = "";  // reset the search field
    };

    const markTodoAsComplete = (index) => {
        todos[index].isComplete = !todos[index].isComplete; //toggle if complete
    };

    const deleteTodo = (index) => {
        let deleteItem = todos[index];
        todos = todos.filter((item) => item !=deleteItem);

    };

    $: console.table(todos);
</script>

<input type="text" placeholder="Add task..." bind:value={task} />
<button on:click={addTodo}>Add</button>

<ol>
    {#each todos as item, index}
        <li class:complete={item.isComplete}>
            <span>
                {item.task}
            </span>
            <span>
               <button on:click={() => markTodoAsComplete(index)}>✅</button>
               <button on:click={() => deleteTodo(index)}>❌</button> 
            </span>
        </li>  
    {/each}
</ol>

<style>
    .complete {
        text-decoration: line-through;
    }
</style>