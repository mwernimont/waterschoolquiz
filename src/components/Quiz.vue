<template>
    <div id="container">
        <div id="Celebration" v-show="Celebration">
            <h1>Correct!</h1>
            <div id="celebrationExplanation"></div>
            <button class="continue">Continue Quiz</button>
        </div>
        <div id="Shame" v-show="Shame">
            <h1>Incorrect...</h1>
            <div id="shameExplanation"></div>
            <button class="continue">Continue Quiz</button>
        </div>
        <div id="result" v-show="ShowResult">
            <div id="message"></div>
            <div id="answerResults">
                <div id="answersCorrect"></div>
                <div id="answersIncorrect"></div>
            </div>
        </div>
        <div id="quiz">
            <div id="results">
                <div id="correct"></div>
                <div id="incorrect"></div>
            </div>
            <div id="questionArea">
                <div id="questionNumber"></div>
                <div id="question"></div>
            </div>
            <div id="options">
                <div id="true">
                    <button class="option">True</button>
                </div>
                <div id="false">
                    <button class="option">False</button>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import quizData from "../assets/quiz.json";
export default {
    name: "Quiz",
    data(){
        return{
            ShowResult: false,
            Celebration: false,
            Shame: false
        } 
    },
    mounted(){
        this.Quiz();
    },
    methods:{
        Quiz(){
            let correct = 0;
            let incorrect = 0;
            let index = 0;
            let self  = this;
            let questionNumberDiv = document.getElementById("questionNumber");
            let questionDiv = document.getElementById("question");
            let options = document.querySelectorAll("button");
            let correctCount = document.getElementById("correct");
            correctCount.innerHTML = correct;
            let incorrectCount = document.getElementById("incorrect");
            incorrectCount.innerHTML = incorrect;
            let answersCorrectDiv = document.getElementById("answersCorrect");
            let answersIncorrectDiv = document.getElementById("answersIncorrect");
            let message = document.getElementById("message");
            let celebrationExplanation = document.getElementById("celebrationExplanation");
            let shameExplanation = document.getElementById("shameExplanation");
            let continueButton = document.getElementsByClassName("continue");

            let questions = [];
            let answers = [];
            let explanations = [];

            quizData.forEach(function(currentQuestion){
                questions.push(currentQuestion.Question);
                answers.push(currentQuestion.Answer);
                explanations.push(currentQuestion.Explanation);
            });

            options.forEach(function(option){
                option.onclick = function(){
                    CheckAnswer(option.innerHTML.toLowerCase());
                }
            })

            function CreateQuestion(){
                questionNumberDiv.innerHTML = "Question #" + (index + 1);
                questionDiv.innerHTML = questions[index];
            }

            function CheckAnswer(answer){
                if(answers[index].toString() === answer){
                    correct++;
                    correctCount.innerHTML = correct;
                    self.Celebration = true;
                    celebrationExplanation.innerHTML = explanations[index];
                }else{
                    incorrect++;
                    incorrectCount.innerHTML = incorrect;
                    self.Shame = true;
                    shameExplanation.innerHTML = explanations[index];
                }
                index++;
                
                    CreateQuestion();
            }

            continueButton.forEach(function(button){
                button.onclick = function(){
                    if(index < 15){
                        self.Celebration = false;
                        self.Shame = false;
                    }else{
                        Results();
                    } 
                }
            })

            function Results(){
                self.ShowResult = true;
                if(correct > 7){
                    message.innerHTML = "Congrats! You know your water!"
                }else{
                    message.innerHTML = "Perhaps you should brush up on your water?"
                }
                answersCorrectDiv.innerHTML = correct;
                answersIncorrectDiv.innerHTML = incorrect;
            }

            CreateQuestion();
        }
    }
}
</script>
<style lang="scss">
    $width: 60vw;
    $Color: #fff;
    #container{
        position: relative;
        font-family: sans-serif;
    }
    #Celebration,
    #Shame,
    #result{
        width: 100vw;
        height: 100vh;
        position: absolute;
        display: flex;
        flex-direction: column;
        justify-content: center;
        

        h1{
            margin: 0;
        }
    }
    #Celebration{
        color: $Color;
        align-items: center;
        background: green;
    }
    #Shame{
        color: $Color;
        align-items: center;
        background: red;
    }
    #celebrationExplanation,
    #shameExplanation{
        width: $width;
        line-height: 2em;
        margin: 50px 0 50px 0;
    }
    .continue{
        background: #fff;
        min-width: 100px;
        height: 50px;
        padding: 10px;
        border-radius: 5px;
        border: none;
        outline: none;
        font-size: 1.2em;
    }
    #result{
        background: #fff;
        display: flex;
        flex-direction: column;
        justify-content: center;
        text-align: center;

        #message{
            font-size: 2em;
            margin-bottom: 20px;
        }

        #answerResults{
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 3em;
        }

        #answersCorrect,
        #answersIncorrect{
            flex: 1;
        }
    }
    #quiz{
        width: 100vw;
        height: 100vh;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }
    #results{
        width: $width;
        height: 40px;
        display: flex;
        align-items: center;
        font-size: 1.5em;
        text-align: center;
        margin-bottom: 50px;

        #correct,
        #incorrect{
            flex: 1;
            padding: 0 10px;
        }
    }
    #questionArea{
        width: $width;
        display: flex;
        flex-direction: column;
        margin-bottom: 50px;
        line-height: 2em;

        #questionNumber{
            font-size: 1.2em;
            margin-bottom: 5px;
        }
        #question{
            flex: 1;
            font-size: 1.4em;
        }
    }
    #options{
        width: $width;
        display: flex;
        justify-content: center;
        align-items: center;

        #true,
        #false{
            flex: 1;
            padding: 10px;
            text-align: center;
        }

        .option{
            width: 40%;
            height: 40px;
            border-radius: 5px;
            background: #003366;
            color: #fff;
            font-size: 1em;
            border: none;
            outline: none;
        }
    }
</style>