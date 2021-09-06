<template>
    <div class='registration'>
        <div id=header>

        </div>
        <body>
            <h1>Welcome to WRCC! Create an account here!</h1>
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
                            <label for="acct_name">Account Name</label>
                            <input v-model.trim="signupForm.acct_name" type="text" placeholder="Must be a minimum of 5 characters" id="acct_name" size="10"/>
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
                        <label for="password">Password</label>
                        <input v-model.trim="signupForm.password" type="password" placeholder="12 or more characters, 1 or more numbers, 1 or more special characters" id="password" />
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
        </body>
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
            else if (!this.validateAcctName(this.signupForm.acct_name)) {
                this.signupForm.errors.push('*Account name must be at least 5 characters in length.');
            }

            if(!this.signupForm.email) {
                this.signupForm.errors.push("*Email required");
                // window.alert("*Email required");
            }
            else if(!this.validateEmail(this.signupForm.email)) {
                this.signupForm.errors.push('*Valid email required.');
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
            else if(!this.validatePhone(this.signupForm.phone)) {
                this.signupForm.errors.push("*Invalid phone number: Must be of form XXX-XXX-XXXX");
            }

            if(!this.signupForm.password) {
                this.signupForm.errors.push("*Password required");
                // window.alert("*Password required");
            }
            if(!this.signupForm.confirmPassword) {
                this.signupForm.errors.push("*You must confirm your password");
                // window.alert("*You must confirm your password");
            }
            if(this.signupForm.password && this.signupForm.confirmPassword && 
              !this.equalPassword(this.signupForm.password, this.signupForm.confirmPassword)) {
                this.signupForm.errors.push("*Passwords do not match");
            }

            // if p or cp aren't input
            //     if p isn't inputted
            //         error p
            //     if cp isn't input
            //         error p
            // else if (both were input)
            //     if p != cp
            //         error p != cp
            //     else p == cp
                    // check character rules 

            // window.alert(this.signupForm.errors.length);s
            // window.alert(this.signupForm.errors[0]);
            e.preventDefault()      
        },

        validateAcctName:function(acct_name) {
            if(acct_name.length < 5) {
                return false;
            } 
            return true;
        },

        validateEmail:function(email) {
            var re = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
            return re.test(email);
        },

        validatePhone:function(phone) {
            var regex= /^(1-)?\d{3}-\d{3}-\d{4}$/;
            return regex.test(phone);
        },

        equalPassword:function(pass1, pass2) {
            return pass1 === pass2;
        }

    }
}
</script>