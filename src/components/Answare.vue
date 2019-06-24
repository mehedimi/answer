<template>
    <div class="answare-section">
        <template v-if="isLoading">
            <h1>Loading...</h1>
        </template>

        <template v-else>
            <h1>{{ answare.answer | capitalize }}</h1>
            <img :src="answare.image" alt="" loading="lazy">
        </template>
        
    </div>
</template>

<script>
    export default {
        props: {
            answare: {
                type: Object,
                default: () => ({})
            },
            isLoading: {
                type: Boolean,
                default: false
            }
        }   
    }
</script>

<style lang="scss">
    .answare-section{
        text-align: center;
        img{
            max-width: 100%;
            border: 1px solid #ddd;
            background-color: #ddd;
            padding: 10px;
            border-radius: 4px;
        }
    }
</style>


