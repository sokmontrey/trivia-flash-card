<script>
    import Card from './Card.svelte';
    export let data;

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
    const numPossibleAnswer = 6; 
    let listOfAnswer = createListOfAnswer(data.length-1, numPossibleAnswer, questionIndex); 
    function nextQuiz(){
        if(questionIndex<data.length-1) {
            Math.random() > 0.5
                ? questionIndex+=1 
                : questionIndex = Math.floor(Math.random()*data.length);
        }
        listOfAnswer= createListOfAnswer(data.length-1, numPossibleAnswer, questionIndex); 
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

<div class='flex content-center justify-center w-screen h-screen bg-sky-90 p-10
sm:p-5'>
    <Card question={data[questionIndex].Q}
        listOfAnswer={listOfAnswer} 
        nextQuiz={nextQuiz} 
        correctAnswer={data[questionIndex].A}/>
</div>
