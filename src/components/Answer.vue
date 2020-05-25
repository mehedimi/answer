<template>
    <div class="answer-section">
        <Loader v-if="isLoading" />
        <template v-else>
            <img :class="{hide: !isImageLoaded}" @load="isImageLoaded = true" :src="answer.image">
            <Loader v-if="!isImageLoaded" />
            <h1 v-if="isImageLoaded">{{ answer.answer | capitalize }}</h1>
        </template>
    </div>
</template>

<script>
    import Loader from './Loader';

    export default {
        props: {
            answer: {
                type: Object,
                default: () => ({})
            },
            isLoading: {
                type: Boolean,
                default: false
            }
        },
        data() {
            return {
                isImageLoaded: false
            }
        },
        components: { Loader },
        watch: {
            isLoading(loaded) {
                if (!loaded) {
                    this.isImageLoaded = false;
                }
            }
        }
    }
</script>

<style lang="scss">
    .answer-section{
        text-align: center;
        margin-top: 30px;
        img{
            max-width: 100%;
            border: 1px solid #ddd;
            background-color: #ddd;
            padding: 10px;
            border-radius: 4px;
        }
        .hide {
            display: none;
        }
    }
</style>


