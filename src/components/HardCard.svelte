<script>
export let question;
export let correctAnswer;
export let goToNextQuiz;
export let packTitle;
export let packAdder;

let isShowAnswer = false;
let inputAnswer = '';
let regex = '';

$: cleanCorrectAnswer = correctAnswer.replace(/\(([^\)]+)\)/g, "").toLowerCase();

function onCheckAnswer(){
    if(inputAnswer){
        let list = inputAnswer.toLowerCase().split(" ");
        for(let i in list) regex += `(${list[i]})${i<list.length-1?"|":""}`;
    }
    isShowAnswer = true;
}

function onNext(){
    isShowAnswer = false;
    inputAnswer ='';
    regex = '';
    goToNextQuiz();
}

function onButtonPressed(){
    if(isShowAnswer){
        onNext();
    }else{
        onCheckAnswer();
    }
}

</script>

<div class='flex-column rounded-lg
sm:py-3
w-full md:w-11/12 lg:w-7/12 xl:w-6/12'>
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

    {#if isShowAnswer}
        <div class='text-gray-500 text-4xl font-mono'>
            {#if regex}
                {#each cleanCorrectAnswer.split(new RegExp(regex)) as word, index}
                <span class={index%2!==0 ? 'text-green-500' : 'text-gray-500'}>
                    {word || ""}
                </span>
                {/each}
            {:else}
                <span class='text-gray-500'>
                    {cleanCorrectAnswer}
                </span>
            {/if}
        </div>
    {/if}

    <div class='flex-column space-y-3 py-7'>
        <input bind:value={inputAnswer} 
        on:keypress={(event)=>{
            if (event.key === "Enter") {
                onButtonPressed();
            }
        }}
        class={`h-auto py-2 px-6 font-semibold rounded-md border border-slate-400 
        outline-none focus:border-blue-500 w-full
        text-left transition ease-in-out delay-50 `} />
    </div>

    <button 
        on:click={onButtonPressed}
        class={`h-auto py-2 px-6 font-semibold rounded-md border border-slate-400 
        hover:bg-blue-600 hover:text-white
        text-left transition ease-in-out delay-50
        ${isShowAnswer? 'bg-gray-900' : 'bg-white'}
        ${isShowAnswer? 'text-white' : 'text-gray-900'}`}>
        {isShowAnswer? 'Next' : 'Check'}
    </button><br/>
</div>