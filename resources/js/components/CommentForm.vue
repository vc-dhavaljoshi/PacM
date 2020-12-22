<template>
    <form>
        <label>Name</label><br/>
        <input type="text" v-model="user">
        <br/>
        <label>Comment</label><br/>
        <textarea name="content" v-model="content"></textarea>
        <br/><br/>
        <button type="button" name="post" v-on:click="replyTo(comment)">Post</button>
    </form>
</template>
<script>
    const axios = require('axios');
    export default{
        props: ['comment'],
        data(){
            return{
                content: '',
                user: '',
            }
        },
        methods:{
            replyTo(comment) {
                let data = {
                    content: this.content,
                    post_id: 1,
                    parent_id: (comment) ? comment.id : null,
                    user:this.user
                };
                axios.post('/api/comment/store', data).then(response => {
                   this.content = '';
                   this.user = '';
                });
            }
        }
    }
</script>