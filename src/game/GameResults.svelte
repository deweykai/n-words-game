<script>
    export let words;
    export let lookback;
    export let guesses;
    export let next;

    console.log(words);
    console.log(guesses);

    let checked = [];
    let score = 0;

    for (let i = 0; i < words.length; i++) {
        const word = words[i];
        const guess = guesses[i + lookback];

        let color = "gray";
        if (i < words.length - lookback) {
            if (word == guess) {
                score += 1;
                color = "green";
            } else {
                color = "red";
            }
        }

        checked.push({ word, color });
    }
</script>

<div>
    <ul class="words">
        {#each checked as word}
            <li style="color: {word.color}">
                {word.word}
            </li>
        {/each}
    </ul>

    <h2>Score: {score} / {guesses.length - lookback}</h2>

    <button class="result-button" on:click={next}>Done</button>
</div>

<style>
    div {
        width: 20rem;
    }
    .words {
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        gap: 1rem;
        padding: 0;
        list-style-type: none;
        margin-left: auto;
        margin-right: auto;
    }

    .words > li {
        font-size: 3.2em;
    }

    .result-button {
        width: 100%;
    }
</style>
