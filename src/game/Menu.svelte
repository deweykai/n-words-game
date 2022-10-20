<script>
    export let startGame;

    let gameLength = 10;
    let lookback = 2;

    function submitGame() {
        startGame(gameLength, lookback);
    }
</script>

<form on:submit={submitGame}>
    <div class="layout">
        <div>
            <label for="length">Length:</label>
            <input name="length" type="number" min="1" bind:value={gameLength} />
        </div>
        <div>
            <label for="lookback">Lookback:</label>
            <input name="lookback" type="number" min="1" bind:value={lookback} />
        </div>
        <button type="submit">Start</button>
    </div>
</form>

<style>
    .layout {
        display: grid;
        gap: 1rem;
        grid-template-columns: 1fr 1fr;
    }

    div > button {
        grid-column: span 2;
    }
</style>
