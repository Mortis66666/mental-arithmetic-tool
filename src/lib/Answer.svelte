<script lang="ts">
    export let redirect: CallableFunction;
    export let answer: number;
    let userAnswer: number;

    function checkAnswer() {
        redirect(Number(userAnswer) === answer);
    }
</script>

<h1>What's the answer?</h1>
<input type="text" bind:value={userAnswer} />
<button on:click={checkAnswer}>Submit</button>
