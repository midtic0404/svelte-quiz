<script>
	import Question from './Question.svelte';

    let activeQuestion = 0;
    let score = 0;
    let quiz = getQuiz();

    async function getQuiz() {
        const res = await fetch('https://opentdb.com/api.php?amount=10&category=12&type=multiple');
        const quiz = await res.json();
        return quiz;
    }

    function nextQuestion() {
        activeQuestion = activeQuestion + 1;
    }

    function resetQuiz() {
        score = 0;
        quiz = getQuiz();
    }

    function addToScore() {
        score = score + 1;
    }


</script>

<style>
   
</style>

<div>
    <button on:click={resetQuiz}>Start New Quiz</button>

    <h3>My Score: {score}</h3>
    <h4>Question # {activeQuestion + 1}</h4>

    {#await quiz}
       loading...
    {:then data}
        {#each data.results as question, index}
            {#if index === activeQuestion}
                <Question {addToScore} {nextQuestion} {question}/>
            {/if}
        {/each}
    {/await}



</div>

