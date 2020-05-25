<template>
    <div class="container">
        <form class="question-form" @submit.prevent="getAnsware">
            <input v-model="question" type="text" class="input" placeholder="Ask your yes no question.">
            <button class="button mt-1">Get Answer</button>
        </form>
        <i>Don't forget to put ? mark on your end of the question.</i>
        <Answer :is-loading="isLoading" v-if="hasAnswer" :answer="answer"/>
    </div>
</template>

<script>
    import Answer from './Answer'
    import axios from 'axios'

    export default {
        data(){
            return {
                answer: {},
                api: 'https://yesno.wtf/api',
                question: '',
                isLoading: false
            }
        },
        components: { Answer },
        computed: {
            hasAnswer() {
                return Object.keys(this.answer).length;
            }
        },
        methods: {
            getAnsware() {
                if(this.isInvalid()){
                    return;
                }
                this.isLoading = true

                axios.get(this.api).then(({ data }) => {
                    this.answer = data
                    this.isLoading = false
                })
            },
            isInvalid() {
                if(!this.question){
                    return true;
                }

                return this.question[this.question.length - 1] !== '?';
            }
        }
    }
</script>

<style lang="scss">
    .container {
        max-width: 500px;
        margin: auto;
    }
    .question-form{
        text-align: right;
        display: flex;
        input {
            flex: 1;
        }
    }
    .input {
        box-sizing: border-box;
        width: 100%;
        padding: 10px;
        border: 1px solid #ddd;
        outline: none;
        margin-top: 11px;
        &:focus{
            border-color: #e74c3c
        }
    }
    .button {
        display: inline-block;
        padding: 10px;
        background-color: #e74c3c;
        color: #fff;
        border: 2px solid #e74c3c;
    }
    i {
        color: #aaa;
    }

    .mt-4{
        margin-top: 4em;
    }
    .mt-1{
        margin-top: 1em;
    }
</style>


