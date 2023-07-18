<template>
    <div class="post">
        <div class="d-flex justify-content-between">
            <h3>
                {{ this.title }} 
            </h3>
            <button type="button" class="close" @click='this.delete'>
                <span aria-hidden="true">&times;</span>
            </button>
        </div>
        <p>
            {{ this.text }}
        </p>
    </div>
</template>

<script>
    export default {
        name: "Post",
        props: [
            'title', 
            'text',
        ],
        components: {

        },
        data(){
            
        },
        methods: {
            delete(){
                this.$emit('delete')
            }
        }
    }
</script>

<style>
    .post{
        border: 1px solid black;
        padding: 15px;
        margin-top: 10px;
    }
    .post:last-child{
        margin-bottom: 10px;
    }
</style>