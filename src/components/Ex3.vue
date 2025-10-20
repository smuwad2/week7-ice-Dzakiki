<script>
import axios from 'axios';
    export default { 

       // add code here
       data() {
            return {
                posts: [],
                selectedMood: '',
                subject: '',
                entry: '',
                message: ''
            }
       },
       computed: {
        baseUrl() {
            if (window.location.hostname=='localhost')
                return 'http://localhost:3000'
            else {
                const codespace_host = window.location.hostname.replace('5173', '3000')
                return `https://${codespace_host}`;
            }
        }
    },
    created() { // created is a hook that executes as soon as Vue instance is created
        axios.get(`${this.baseUrl}/posts`)
            .then(response => {
                // this gets the data, which is an array, and pass the data to Vue instance's posts property
                this.posts = response.data
                console.log(this.posts);
            })
            .catch(error => {
                this.posts = [{ entry: 'There was an error: ' + error.message }]
            })
    },
    methods: {
        submitNewPost() {
            const newPost = {
                subject: this.subject,
                entry: this.entry,
                mood: this.selectedMood
            };

            axios.post(`${this.baseUrl}/addPost`, newPost)
                .then(response => {
                    this.message = 'Post added successfully!';
                    this.subject = '';
                    this.entry = '';
                    this.selectedMood = '';
                })
                .catch(error => {
                    this.message = 'There was an error submitting the post:' + error.message;
                });
        }
    }

    }
</script>

<template>
    <div class="table m-2">
        <h3>Add a New Blog Post</h3>

        Subject: <input type='text' size='30' v-model='subject' required>
        <br>

        Entry: <br>
        <textarea name='entry' cols='80' rows='5' v-model='entry' required></textarea>
        <br>

        Mood:
        <!-- TODO: Build a dropdown list here for selecting the mood -->
        <select v-model="selectedMood">
            <option v-for="post in posts">{{ post.mood }}</option>
        </select>
        <br>

        <br>
        <button @click="submitNewPost">Submit New Post</button>

        <p v-if="message">{{ message }}</p>

        <hr> Click  <a><router-link to="/ViewPosts/">here</router-link></a>  to return to Main Page
       
    </div>
</template>

