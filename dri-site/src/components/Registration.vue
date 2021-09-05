<template>
    <div class='registration'>
        <div id=body>
            <h1>Welcome to DRI! Get Started! Create an account here!</h1>
            <div id='formContainer'>
                
                <form  @submit="validateSignup"  novalidate='true'>

                    <div id='errorContainer' >
                        <p v-if='signupForm.errors.length'>
                            <b>Please correct the following error(s):</b> 

                            <ul>   
                                <li v-for="error in signupForm.errors" v-bind:key="error.id">{{ error }}</li>
                            </ul>
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
                        <input v-model.trim="signupForm.confirmPassword" type="password" placeholder="" id="confirmPassword" />
                    </div>

                    <div id='fieldContainer'>
                        <button @click="validateSignup" class="button">Sign Up</button>
                    </div>

                </form>
            

            </div>
        </div>
    </div>
    
</template>

<script>
export default {
    e1: '#app',

    data() {
        return {
            signupForm: {
                errors: [],
                acct_name: null,
                email: null,
                first: null,
                last: null,
                phone: null,
                password: null,
                confirmPassword: null
            }
        }
    },

    methods: {

        validateSignup:function(e) {
            this.signupForm.errors = [];
            if(!this.signupForm.acct_name) {
                this.signupForm.errors.push("*Account name required");
                // window.alert("*Account name required");
            }

            if(!this.signupForm.email) {
                this.signupForm.errors.push("*Email required");
                // window.alert("*Email required");
            }
            else if(!this.validateEmail(this.signupForm.email)) {
                this.signupForm.errors.push('Valid email required.');
            }

            if(!this.signupForm.first) {
                this.signupForm.errors.push("*First name required");
                // window.alert("*First name required");
            }

            if(!this.signupForm.last) {
                this.signupForm.errors.push("*Last name required");
                // window.alert("*Last name required");
            }

            if(!this.signupForm.phone) {
                this.signupForm.errors.push("*Phone number required");
                // window.alert("*Phone number required");
            }

            if(!this.signupForm.password) {
                this.signupForm.errors.push("*Password required");
                // window.alert("*Password required");
            }

            if(!this.signupForm.confirmPassword) {
                this.signupForm.errors.push("*You must confirm your password");
                // window.alert("*You must confirm your password");
            }
            
            // window.alert(this.signupForm.errors.length);

            // if (!this.errors.length) {
            //     return true;
            // }
            
            // window.alert(this.signupForm.errors[0]);
            e.preventDefault()      
        },

        // validateAccName

        validateEmail:function(email) {
            var re = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
            return re.test(email);
        }
    }
}
</script>