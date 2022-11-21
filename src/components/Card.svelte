<script>
export let question;
export let listOfAnswer;
export let nextQuiz;
export let correctAnswer;

let isShowAnswer = false;
</script>

<div class='flex-column rounded-lg
sm:px-10 md:px-20
sm:py-5 md:py-10
sm:w-screen md:w-3/4 lg:w-1/2 xl:w-5/12'>
    <a href='/'>
        <button class='pb-5 hover:text-blue-500 transition ease-in-out delay-100'>Back</button>
    </a>
    <h1 class='font-serif border-b text-xl pb-10'>{question}</h1>

    <div class='flex-column space-y-5 py-10'>
        {#each listOfAnswer as answer}
            <button on:click={()=>{ isShowAnswer = true; }} 
                class={`h-auto py-2 px-6 font-semibold rounded-md border border-slate-200 
                ${isShowAnswer? '': 'hover:bg-gray-50 hover:border-blue-500'}
                ${isShowAnswer? correctAnswer===answer?'bg-green-50 text-lime-500':'text-red-200':''}
                ${isShowAnswer? correctAnswer===answer?'shadow-md shadow-lime-50':'':''}
                transition ease-in-out delay-50 `}>
                {answer}
            </button><br/>
        {/each}
    </div>

    <button class={`h-10 px-6 font-semibold rounded-md white transition ease-in-out delay-50 hover:bg-blue-500
    bg-black text-white disabled:hidden`} disabled={!isShowAnswer}
    on:click={()=>{isShowAnswer=false; nextQuiz();}}>Next</button>
</div>