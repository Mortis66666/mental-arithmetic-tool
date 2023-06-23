<script lang="ts">
    import NumberCard from "./lib/NumberCard.svelte";
    import Answer from "./lib/Answer.svelte";
    import EndScreen from "./lib/EndScreen.svelte";

    let minNum: number = 0;
    let maxNum: number = 9;
    let numAmt: number = 10;
    let displayTime: number = 0.2;
    let delay: number = 0.3;
    let num: number | "" = "";
    let sum: number = 0;
    let correct: boolean;

    let phase: "input" | "start" | "answer" | "end" = "input";

    async function wait(seconds: number) {
        await new Promise(resolve => setTimeout(resolve, seconds * 1000));
    }

    function randomRange(min: number, max: number): number {
        return Math.floor(Math.random() * (max - min + 1)) + min;
    }

    function checkValid(e: Event) {
        console.log(minNum);
    }

    async function start() {
        phase = "start";

        for (let i = 0; i < numAmt; i++) {
            num = randomRange(Number(minNum), Number(maxNum));
            sum += num;

            await wait(displayTime);

            num = "";

            await wait(delay);
        }

        phase = "answer";
    }

    function redirectToEndScreen(result: boolean) {
        correct = result;
        phase = "end";
    }

    function reset() {
        phase = "input";
        sum = 0;
        correct = undefined;
    }
</script>

<main>
    {#if phase == "input"}
        <label for="min-num">Minimum number: </label>
        <input
            type="text"
            name="min-num"
            bind:value={minNum}
            on:change={checkValid}
        />

        <br />

        <label for="max-num">Maximum number:</label>
        <input
            type="text"
            name="max-num"
            bind:value={maxNum}
            on:change={checkValid}
        />

        <br />

        <label for="num-amt">Amount of numbers to display:</label>
        <input type="text" name="num-amt" bind:value={numAmt} />

        <br />

        <label for="display-time">Time taken to display each number:</label>
        <input type="text" name="display-time" bind:value={displayTime} />
        <p>seconds</p>

        <br />

        <label for="delay">Time taken until next number is displayed:</label>
        <input type="text" name="delay" bind:value={delay} />
        <p>seconds</p>

        <br />

        <button on:click={start}>Start</button>
    {:else if phase == "start"}
        <NumberCard {num} />
    {:else if phase == "answer"}
        <Answer redirect={redirectToEndScreen} answer={sum} />
    {:else}
        <EndScreen {correct} answer={sum} {reset} />
    {/if}
</main>

<style>
    label {
        font-weight: bold;
    }

    input[type="text"] {
        margin-bottom: 10px;
        padding: 5px;
    }

    p {
        display: inline;
    }

    main {
        font-family: Arial, sans-serif;
        padding: 20px;
    }
</style>
