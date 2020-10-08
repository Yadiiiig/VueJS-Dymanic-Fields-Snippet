<template>
    <section id="app" class="section">
    <b-container>
        <b-card title="Create questions">
            <b-card-text>
                <form>
                    <div v-for="question in questions" :key="question.id">
                        <b-button variant="success" a @click="addAnswer(question.id)">+ Add Answer</b-button>
                        <b-button variant="danger" @click="removeQuestion(question.id)">+ Remove Question</b-button>
                        <br>
                        <label class="label">{{ question.title }}</label>
                        <div v-for="answer in question.answers" :key="answer.id">
                            <b-input-group style="max-width:500px">
                                <b-form-input type="text" placeholder="Type answer option here" v-model="answer.content"></b-form-input>
                                <template v-slot:append>
                                    <b-button variant="danger" @click="removeAnswer(question.id, answer.id)">- Remove answer</b-button>
                                </template>
                                <br>
                                <br>
                            </b-input-group>
                        </div>
                    </div>
                <input 
                        placeholder="Type new question here" 
                        v-model="newQuestionTitle" />
                <b-button variant="success" @click="addQuestion">+ Add Question</b-button>
                </form>
            </b-card-text>  
        </b-card>  

            <div class="column">
                <h5>
                    JSON
                </h5>
                <pre><code>{{newQuestionTitle}}</code></pre>
                <pre><code>{{questions}}</code></pre>
            </div>

    </b-container>
</section>

</template>

<script>
    export default {
        data() { return {
            newQuestionTitle: "",
            questions: [
                
            ]
        }},
        
    methods: {
        addQuestion(){
            let newID = this.questions.length == 0 ? 0 : this.questions[this.questions.length - 1].id + 1;
            this.questions.push({
                "id": newID,
                "title": this.newQuestionTitle,
                "answers": [
                    { "id": 0, "content": ""  }
                ]
        });
        this.newQuestionTitle = "";
        },
        removeQuestion(id) {
            this.questions = this.questions.filter(elm => elm.id != id);
        },
        addAnswer(questionID) {
            let newID = this.questions[questionID].answers.length == 0 ? 0 : this.questions[questionID].answers[this.questions[questionID].answers.length - 1].id + 1;
            this.questions[questionID].answers.push({ "id": newID, "content": ""  });
        },
        removeAnswer(questionID, id) {
            this.questions[questionID].answers = this.questions[questionID].answers.filter(elm => elm.id != id);
    }
  }
    }
</script>
