<script lang="ts">
    export let redirect: CallableFunction;
    export let answer: number;

    function checkAnswer(event: any) {
        redirect(Number(event.target.value) === answer);
    }
</script>

<h1>What's the answer?</h1>
<input type="text" />
<button on:click={checkAnswer}>Submit</button>
