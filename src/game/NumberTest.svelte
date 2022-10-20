<script>
    export let word;
    export let next;
    export let expectInput;

    let guess = "";

    function submitGuess() {
        next(guess.toUpperCase());
        guess = "";
    }
</script>

<form on:submit|preventDefault={submitGuess}>
    <div class="card">
        <div class="word">
            <h1>{word}</h1>
        </div>
        <div class="control">
            {#if expectInput}
                <input bind:value={guess} placeholder="#" />
            {/if}
            <button>Next</button>
        </div>
    </div>
</form>

<style>
    .word {
        height: 5em;
    }
    input {
        width: 3rem;
    }
    .control {
        display: flex;
        gap: 1rem;
    }

    .control > * {
        border-radius: 1rem;
    }
</style>
