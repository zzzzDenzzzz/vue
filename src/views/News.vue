<template>
    <section class="posts">
        <div v-for="(post, index) in this.posts" v-if='this.posts.length'>
            <Post @delete="this.deletePost(post.id)"  :title="post.title" :text="post.text"/>
        </div>
        <div v-else>
            <EmptySection text="Еще нет ни одного поста!"/>
        </div>
        <div class="addForm">
            <div class="border rounded p-3">
                <div class="form-group">
                    <label for="exampleFormControlInput1">
                        Название поста <span class='text-danger'>*</span>
                    </label>
                    <input :class='{ "with-error": this.error.title }' v-model='this.title' type="text" class="form-control">
                    <small v-if='this.error.title' class="form-text text-danger">Заполните заголовок</small>
                </div>
                <div class="form-group">
                    <label for="exampleFormControlTextarea1">
                        Текст <span class='text-danger'>*</span>
                    </label>
                    <textarea :class='{ "with-error": this.error.text }' v-model='this.text' class="form-control"></textarea>
                    <small v-if='this.error.text' class="form-text text-danger">Заполните текст</small>
                </div>
                <button class="btn btn-primary" @click="createPost">
                    Отправить
                </button>
            </div>
        </div>
    </section>
</template>

<script>
    import Post from "@/components/post/Post.vue"
    import EmptySection from "@/components/EmptySection.vue";

    export default {
        name: "News",
        components: {
            Post,
            EmptySection
        },
        data(){
            return {
                title: "",
                text: "",
                error: {
                    title: false,
                    text: false,
                },
                posts: [
                    { id: 1, title: "Пост 1", text: "Какое-то тестовый текст 1"},
                    { id: 2, title: "Пост 2", text: "Какое-то тестовый текст 2"},
                    { id: 3, title: "Пост 3", text: "Какое-то тестовый текст 3"},
                    { id: 4, title: "Пост 4", text: "Какое-то тестовый текст 4"},
                    { id: 5, title: "Пост 5", text: "Какое-то тестовый текст 5"},
                    { id: 6, title: "Пост 6", text: "Какое-то тестовый текст 6"},
                    { id: 7, title: "Пост 7", text: "Какое-то тестовый текст 7"},
                ],
            }
        },
        methods: {
            createPost(){
                if(this.text && this.title){
                    this.posts.push({
                        title: this.title,
                        text: this.text
                    });

                    this.title = "";
                    this.text = "";

                    this.error.title = false;
                    this.error.text = false;
                }else{
                    this.error.title = !this.title;
                    this.error.text = !this.text;
                }
            },
            deletePost(id){
                this.posts = this.posts.filter(post => post.id != id);
            }
        },
        watch: {
            title(value){
                this.error.title = false;
            },
            text(value){
                this.error.text = false;
            }
        }
    }
</script>

<style>
    .posts{
        margin: 0 auto;
        max-width: 80%;
    }
    .addForm{
        margin-top: 15px;
        margin-bottom: 15px;
    }
</style>