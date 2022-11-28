<script>
    import Card from './Card.svelte';
    import HardCard from './HardCard.svelte';

    export let data;
    export let frontmatter;

    let isEasyMode = false;
    function onModeChange(event){
        event.preventDefault();
        isEasyMode = !isEasyMode;
    }

    function shuffleArray (array){
        for (let i = array.length - 1; i > 0; i--) {
            const j = Math.floor(Math.random() * (i + 1));
            const temp = array[i];
            array[i] = array[j];
            array[j] = temp;
        }
    }
    shuffleArray(data);

    let questionIndex = 0;
    const numPossibleChoice= 5; // <--- change here to set how many choice would show up

    let listOfAnswer = createListOfAnswer(data.length-1, numPossibleChoice, questionIndex); 
    function nextQuiz(){
        if(questionIndex<data.length-1) {
            Math.random() > 0.7
                ? questionIndex+=1 
                : questionIndex = Math.floor(Math.random()*data.length);
        }
        listOfAnswer= createListOfAnswer(data.length-1, numPossibleChoice, questionIndex); 
    }

    function createListOfAnswer (range, count, correctIndex) {
        let nums = new Set();
        while (nums.size < count) {
            nums.add(Math.floor(Math.random() * (range - 1 + 1) + 1));
        }
        const indexs = [...nums];
        indexs[Math.floor(Math.random()* indexs.length)] = correctIndex;
        return indexs.map((i)=>{return data[i].A});
    }
</script>

<div class='flex content-center justify-center w-screen h-screen
py-8 px-10
'>
    {#if isEasyMode}
        <Card question={data[questionIndex].Q}
            listOfAnswer={listOfAnswer} 
            nextQuiz={nextQuiz} 
            correctAnswer={data[questionIndex].A}
            packTitle={frontmatter.title}
            packAdder={frontmatter.addedBy}/>
    {:else}
        <HardCard question={data[questionIndex].Q}
            listOfAnswer={listOfAnswer} 
            goToNextQuiz={nextQuiz} 
            correctAnswer={data[questionIndex].A}
            packTitle={frontmatter.title}
            packAdder={frontmatter.addedBy}/>
    {/if}

    <form class='fixed bottom-0 right-0 p-5 px-10 flex content-center justify-center'>
        <p class='font-mono text-gray-400'>Easy Mode:</p>
        <button 
        class={`rounded-xl w-7 h-7 border-2 ml-2 
        transition ease-in-out delay-100 
        hover:bg-gray-300 hover:border-0
        ${isEasyMode?'bg-blue-500':'bg-white'}`}
        on:click={onModeChange}></button>
    </form>
</div>
