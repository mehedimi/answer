<template>
    <div class="container">
        <form class="question-form" @submit.prevent="getAnsware">
            <input v-model="question" type="text" class="input" placeholder="Ask your yes no question.">
            <i>Don't forget to put ? mark on your end of the question.</i>
            <button class="button mt-1">Get Answare</button>
            
        </form>
        <Answare :is-loading="isLoading" v-if="!isEmpty(answare)" :answare="answare"/>
    </div>
</template>

<script>
    import Answare from './Answare'
    import axios from 'axios'

    export default {
        data(){
            return {
                answare: {},
                api: 'https://yesno.wtf/api',
                question: '',
                isLoading: false
            }
        },
        components: { Answare },

        methods: {
            isEmpty(obj){
                return !Object.keys(obj).length;
            },
            getAnsware() {
                if(this.isInvalid()){
                    return;
                }
                this.isLoading = true

                axios.get(this.api).then(({ data }) => {
                    this.answare = data
                    this.isLoading = false
                })
            },
            isInvalid() {
                if(!this.question){
                    return true;
                }

                if(this.question[this.question.length - 1] !== '?'){
                    return true;
                }

                return false;
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
        i{
            text-align: left;
            display: block;
            margin-top: 5px;
            font-size: 14px;
            color: #aaa;
            font-weight: light
        }
    }
    .input {
        box-sizing: border-box;
        width: 100%;
        padding: 10px;
        border: 1px solid #ddd;
        outline: none;
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

    .mt-4{
        margin-top: 4em;
    }
    .mt-1{
        margin-top: 1em;
    }
</style>


