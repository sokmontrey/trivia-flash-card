<script>
export let question;
export let listOfAnswer;
export let nextQuiz;
export let correctAnswer;
export let packTitle;
export let packAdder;

let isShowAnswer = false;
</script>

<div class='flex-column rounded-lg
sm:py-3
w-full md:w-8/12 lg:w-7/12 xl:w-6/12'>
    <a href='/'>
        <button class='pb-3 
        text-blue-400 underline underline-offset-8 hover:text-blue-500 transition ease-in-out delay-50'>Back</button>
    </a>
    <p class='text-stone-400 text-lg'>
        {packTitle}
    </p>
    <p class='border-b-2 pb-5 text-stone-400 text-sm'>
        added by: {packAdder}
    </p>

    <h1 class='font-serif text-xl pb-3 pt-6'>{question}</h1>

    <div class='flex-column space-y-3 py-7'>
        {#each listOfAnswer as answer}
            <button on:click={()=>{ isShowAnswer = true; }} 
                class={`h-auto py-2 px-6 font-semibold rounded-md border border-slate-400 
                ${isShowAnswer? '': 'hover:bg-gray-50 hover:border-blue-500'}
                ${isShowAnswer? correctAnswer===answer?'bg-green-50 text-lime-500':'text-red-200':''}
                ${isShowAnswer? correctAnswer===answer?'shadow-md shadow-lime-50':'':''}
                text-left transition ease-in-out delay-50 `}>
                {answer}
            </button><br/>
        {/each}
    </div>

    <button class={`h-10 px-6 font-semibold rounded-md white transition ease-in-out delay-50 hover:bg-blue-500
    bg-black text-white mb-20 disabled:hidden`} disabled={!isShowAnswer}
    on:click={()=>{isShowAnswer=false; nextQuiz();}}>Next</button>
</div>