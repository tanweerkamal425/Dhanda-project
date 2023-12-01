<template>
    <div class="index-page">
        <div class="party-form">
        <img class="dhanda-img" src="/assets/img/dhanda.png" alt="dhanda-image" />
        <AppNavbar page="party" />
        <h3 class="form-heading">Create Party</h3>
        <div class="form-container">
        <form>
            <fieldset>
                <label for="first-name">First name:
                    <input v-model="post.first_name" class="input" type="text" id="first-name" name="first-name" placeholder="Enter your name..." required />
                </label>
                <label for="last-name">Last name:
                    <input v-model="post.last_name" class="input" type="text" id="last-name" name="last-name" placeholder="Enter your name..." required />
                </label>
                <label for="phone">Phone:
                    <input v-model="post.phone" class="input" type="text" id="phone" name="phone" max="10" placeholder="e.g, 9331234567" required />
                </label>
                <label for="amount">Amount:
                    <input v-model.number="post.amount" class="input" type="text" id="amount" name="amount" placeholder="5000" required />
                </label>
            </fieldset>
            <FormErrorMessage :errors="validationErrors" />
            <button @click.prevent="createPost" class="button">Save</button>
        </form>
        </div>
       
    </div>
    </div>
    
</template>

<script>
import AppNavbar from '@/components/AppNavbar.vue';
import FormErrorMessage from '@/components/FormErrorMessage.vue';

let postModel = {
    first_name: "",
    last_name: "",
    phone: "",
    amount: "",
}
    export default {
        components: {
            AppNavbar,
            FormErrorMessage,
        },
        
        data() {
            return {
                post: { ...postModel }, //to be noted...
                validationErrors: [],
            }
        },

        methods: {
            createPost() {
                const url = '/api/v1/parties'
                const options = {
                    method: "POST",
                    body: JSON.stringify(this.post),
                };

                fetch(url, options).then((res) => {
                    if (!res.ok) {
                        return Promise.reject(res);
                    }
                    return res.json();
                }).then((data) => {
                    console.log(data);
                    this.$router.push({
                        name: "party.detail",
                        params: {
                            id: data.id,
                        }
                    });
                }).catch((error) => {
                    error.json().then((e) => {
                        this.validationErrors = [e.msg];
                    });
                });
            }
        }
    }
</script>