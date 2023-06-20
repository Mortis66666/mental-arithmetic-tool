<script lang="ts">
    interface ResetFunction {
        (
            event: MouseEvent & {
                currentTarget: EventTarget & HTMLButtonElement;
            }
        ): void;
    }

    export let correct: boolean;
    export let answer: number;
    export let reset: ResetFunction = event => {};
</script>

{#if correct}
    <h1>Congratz!</h1>
    <h3>
        The answer was {answer} and you get it correct, keep up the good word!
    </h3>
{:else}
    <h1>Unfortunate</h1>
    <h3>
        The answer was {answer} and you get it wrong, better luck next time!
    </h3>
{/if}

<button on:click={reset}>Reset</button>
