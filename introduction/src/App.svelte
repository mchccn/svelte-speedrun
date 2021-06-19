<script lang="ts">

let todo = "";

let input!: HTMLInputElement;

let todos = [] as {
        todo: string;
        completed: boolean;
}[];

function addTodo(todo: string) {
        todos = [{ todo, completed: false }, ...todos];
 
        todo = "";

        input.value = "";
}

function removeTodo(index: number) {
        todos = todos.filter((_, i) => i !== index);
}

</script>

<svelte:window on:keypress={(e) => e.key === "Enter" && todo ? addTodo(todo) : void 0} />

<main>

        <h1>a cool todolist app in svelte</h1>

        <input bind:this={input} bind:value={todo} type="text" />

        {#if todo}
                <input on:click={() => addTodo(todo)} type="submit" value="add" />
        {/if}

        <ul>
                {#each todos as todo, index}
                        <li>
                                <span>{todo.todo}</span>
                                <button on:click={() => removeTodo(index)}>🗑</button>
                        </li>   
                {/each}
        </ul>
</main>
