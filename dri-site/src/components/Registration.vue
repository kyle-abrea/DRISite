<template>
    <div class='registration'>
        <div id=body>
            <h1>Welcome to DRI! Get Started! Create an account here!</h1>
            <div id='formContainer'>
                
                <form @submit='validateSignup' novalidate="true">

                    <div id='fieldContainer' v-if='signupForm.errors.length'>
                        <p>
                            <b>Please correct the following error(s):</b> 
                            <!-- <ul>   
                                <li v-for="error in signupForm.errors">{{ error }}</li>
                            </ul> -->
                        </p>
                    </div>

                    <div id='fieldContainer'>
                            <label for="acct_name">Account Name: </label>
                            <input v-model.trim="signupForm.acct_name" type="text" placeholder="" id="acct_name" />
                    </div>

                    <div id='fieldContainer'>
                        <label for="email">Email: </label>
                        <input v-model.trim="signupForm.email" type="text" placeholder="" id="email" />
                    </div>
                    
                    <div id='fieldContainer'>
                        <label for="first">First Name: </label>
                        <input v-model.trim="signupForm.first" type="text" placeholder="" id="first" />
                    </div>

                    <div id='fieldContainer'>
                        <label for="last">Last Name: </label>
                        <input v-model.trim="signupForm.last" type="text" placeholder="" id="last" />
                    </div>

                    <div id='fieldContainer'>
                        <label for="phone">Phone Number: </label>
                        <input v-model.trim="signupForm.phone" type="text" placeholder="" id="phone" />
                    </div>

                    <div id='fieldContainer'>
                        <label for="password">Password: </label>
                        <input v-model.trim="signupForm.password" type="password" placeholder="" id="password" />
                    </div>

                    <div id='fieldContainer'>
                        <label for="password">Confirm Password: </label>
                        <input v-model.trim="signupForm.confirmPassword" type="password" placeholder="" id="password" />
                    </div>

                    <div id='fieldContainer'>
                        <button @click="signup" class="button">Sign Up</button>
                    </div>

                </form>
            

            </div>
        </div>
    </div>
    
</template>

<script>
export default {
    data() {
        return {
            signupForm: {
                errors: [],
                acct_name: '',
                email: '',
                first: '',
                last: '',
                phone: '',
                password: '',
                confirmPassword: ''
            }
        }
    },

    methods: {

        validateSignup:function() {
            this.errors = [];
            if(!this.signupForm.acct_name)
                this.errors.push("Account name required");

            if(!this.signupForm.email)
                this.errors.push("Email required");

            if(!this.signupForm.first)
                this.errors.push("First name required");

            if(!this.signupForm.last)
                this.errors.push("Last name required");

            if(!this.signupForm.phone)
                this.errors.push("Phone number required");

            if(!this.signupForm.password)
                this.errors.push("Password required");

            if(!this.signupForm.confirmPassword)
                this.errors.push("You must confirm your password");
              
        }
    }
}
</script>