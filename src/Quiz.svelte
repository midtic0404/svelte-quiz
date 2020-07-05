<script>
    let result = null;
    let correctAnswer = 'b';
    let answers = ['a', 'b', 'c', 'd'];
    let quiz = getQuiz();

    function pickAnswer(answer) {
        if(answer === correctAnswer) {
            result = 'Correct!';
            return;
        }
        result = 'Oops!';
        
    }

    async function getQuiz() {
        const res = await fetch('https://opentdb.com/api.php?amount=10&category=12&type=multiple');
        const quiz = await res.json();
        return quiz;
    }

    function handleClick() {
        quiz = getQuiz();
    }


</script>

<style>
    /* h4 {
        color: red;
    } */
</style>

<div>
    <button on:click={handleClick}>Get Quiz</button>
    {#if result}
        <h4>{result}</h4>
    {:else}
        <h4>please pick an answer</h4>
    {/if}

    {#await quiz}
       loading...
    {:then data}
        <h3>{data.results[0].question}</h3>
    {/await}


    {#each answers as answer}
        <button on:click={() => pickAnswer(answer)}>Answer {answer.toUpperCase()}</button>
    {/each}

</div>

