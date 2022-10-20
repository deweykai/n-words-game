<script>
    import NumberTest from "./NumberTest.svelte";
    import GameResults from "./GameResults.svelte";
    import Menu from "./Menu.svelte";

    const A = "A".charCodeAt(0);
    const Z = "Z".charCodeAt(0);

    function randomChar() {
        const range = Z - A;
        const base = A;
        const charCode = base + Math.random() * range;
        return String.fromCharCode(charCode);
    }

    let gameLength = 0;
    let lookback = 2;

    let state = "menu";

    let words = [];
    let guesses = [];
    let currentWord = randomChar();
    $: expectInput = words.length >= lookback;

    function next(guess) {
        words = [...words, currentWord];
        guesses = [...guesses, guess];

        currentWord = randomChar();

        if (words.length >= gameLength + lookback) {
            state = "results";
        }
    }

    function resultsChecked() {
        state = "menu";
    }

    function startGame(length, lookbackValue) {
        state = "game";
        gameLength = length;
        lookback = lookbackValue;
        words = [];
        guesses = [];
        currentWord = randomChar();
    }
</script>

{#if state == "game"}
    <NumberTest {expectInput} word={currentWord} {next} />
{:else if state == "results"}
    <GameResults {words} {guesses} {lookback} next={resultsChecked} />
{:else if state == "menu"}
    <Menu {startGame} />
{:else}
    <h1>Invalid state</h1>
{/if}
