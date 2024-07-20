<script lang="ts">
    import {writable} from "svelte/store";

    const messages = writable<string[]>([]);

    const url = "ws://localhost:8080/ws";

    const ws = new WebSocket(url);
    ws.onopen = () => {
        console.log("Connected to the server");
    };
    ws.onmessage = (event) => {
        console.log(event.data);
        messages.update((messages) => [...messages, JSON.parse(event.data).message]);
    };
    

let name: string | null = null;
</script>


<input bind:value={name} placeholder="Enter your name" />
<!-- <button on:click={() => name ? (messages = [...messages, `Hello ${name}!`]) : null}> Say hello </button> -->

{#each $messages as message, i (i)}
	<p>{message}</p>
{/each}
