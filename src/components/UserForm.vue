<template>
    <form @submit.prevent>
		<h4>Register with us</h4>
		<input 
            class="input"
			v-model="newUser.name.first"
			type="text"
			placeholder="Name"
			>
		<input
            class="input"
			v-model="newUser.name.last"
			type="text"
			placeholder="Surname"
			>
		<textarea 
            class="textarea"
            v-model="newUser.about"
			cols="30" 
			rows="3"
			placeholder="Tell us about yourself"
			></textarea>
		<button
            class="btn btn-outline-primary"
            @click="createUser"
        >Create</button>
	</form>
</template>

<script>
import {v4} from 'uuid';
    export default {
        data() {
            return {
                newUser: {
                    name: {
                        first: "",
                        last: ""
                    },
                    about: "",
                }
            }
        },
        methods: {
            createUser() {
                
                const options = { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric', hour: 'numeric', minute: 'numeric', };
                const mow  = new Date();

                this.newUser._id = v4();
                this.newUser.registered = mow.toLocaleDateString("en-US", options);
                this.newUser.tags =  [
                        "commodo",
                        "eiusmod"
                    ]
                this.$emit('create', this.newUser);
                this.newUser =  {
                    name: {
                        first: "",
                        last: ""
                    },
                    about: ""
                }
            }
        }
    }
</script>

<style lang="scss">

form {
    display: flex;
    flex-direction: column;
	width: 40%;
    margin: 0 auto;
    h4 {
        text-align: center;
        color: #0a5084;
        font-weight: bold;
    }
    .textarea, .input {
        width: 100%;
        border: 1px solid #0a5084;
        padding: 10px 15px;
        margin-top: 15px; 
        resize: none;
    }
    .btn {
        padding: 10px 15px;
        background: none;
        color: #0a5084;
        border: 1px solid #0a5084;
        margin-top: 10px;
    }
    .btn-outline-primary {
        --bs-btn-hover-bg: #0a5084;
        --bs-btn-hover-border-color: #0a5084;
    }
}
</style>