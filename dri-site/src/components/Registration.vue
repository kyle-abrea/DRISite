<template>
    <div class='registration'>
        <body>         
            <!-- user isn't registered yet, so render the form container while they're registering -->
            <div id='formContainer' v-if='!requestHandler.registered'>
                <h1>Welcome to WRCC! Create an account here!</h1>     

                <!-- registration form starts here -->
                <form  @submit="register"  method='post' novalidate='true'>

                    <!-- displaying registration errors starts here -->
                    <div id='errorContainer' >
                        <p v-if='errorHandler.errors.length'>
                            <b>Please correct the following error(s):</b> 

                            <ul>   
                                <li v-for="error in errorHandler.errors" v-bind:key="error.id">{{ error }}</li>
                            </ul>
                        </p>    
                    </div>
                    <!-- displaying registration errors ends here -->

                    <div id='fieldContainer'>
                            <label for="acct_name">Account Name:*</label>
                            <input v-model.trim="signupForm.acct_name" type="text" placeholder="Must be a minimum of 5 characters" id="acct_name" size="10"/>
                    </div>

                    <div id='fieldContainer'>
                        <label for="email">Email:* </label>
                        <input v-model.trim="signupForm.email" type="text" placeholder="example@example.com" id="email" />
                    </div>
                    
                    <div id='fieldContainer'>
                        <label for="first">First Name:*</label>
                        <input v-model.trim="signupForm.first" type="text" placeholder="First" id="first"/>
                    </div>

                    <div id='fieldContainer'>
                        <label for="last">Last Name:*</label>
                        <input v-model.trim="signupForm.last" type="text" placeholder="Last" id="last"/>
                    </div>

                    <div id='fieldContainer'>
                        <label for="phone">Phone Number:*</label>
                        <input v-model.trim="signupForm.phone" type="text" placeholder="XXX-XXX-XXXX (Must contain dashes)" id="phone" />
                    </div>

                    <div id='fieldContainer'>
                        <label for="password">Password:*</label>
                        <input v-model.trim="signupForm.passwd" type="password" placeholder="At least 12 characters, must consist of letters, numbers, or special characters" id="password" />
                    </div>

                    <div id='fieldContainer'>
                        <label for="password">Confirm Password:*</label>
                        <input v-model.trim="errorHandler.confirmPassword" type="password" placeholder="At least 12 characters, must consist of letters, numbers, or special characters" id="confirmPassword" />
                    </div>

                    <div id='fieldContainer'>
                        <button @click="register" class="button">Sign Up</button>
                    </div>

                </form>
                <!-- registration form ends here -->
            </div>
            
            <!-- user has successfully registered and made an account, so un-render the form container and render a success response UI -->
            <div id='successContainer' v-if='requestHandler.registered'>
                <h1>Successfully created account!</h1>
                <!-- dummy button to demonstrate that user should log in with their new account right after successful registration -->
                <div id='fieldContainer'>
                    <button class="button">Click here to log in!</button> 
                </div>
            </div>
        </body>
        <!-- loading transition -->
        <transition name="fade">
            <div v-if="loading" class="loading">
                <p>Loading...</p>
            </div>
        </transition>
    </div>
    
</template>

<script>

// for post requests
import axios from 'axios'

export default {
    data() {
        return {          
            loading: false,

            requestHandler: {
                url: "https://wrcc.dri.edu/pass",
                registered: false
            },
            
            errorHandler: {
                errors: [],
                confirmPassword: null
            }, 

            signupForm: {
                session_id: "",
                svc: "acct",
                subsvc: "acct_create",
                acct_name: null,
                email: null,
                first: null,
                last: null,
                phone: null,
                passwd: null,
            },
        }
    },

    methods: {
        // function to register a user
        register:function(e) {
            window.alert("hell0 world");
            this.loading = true;
            
            if(this.validateSignup(e)) {
                axios.post(this.requestHandler.url, this.signupForm, {
                                headers: { 'Content-Type': 'application/x-www-form-urlencoded' }
                            })
                            .then((result) => { 
                                this.loading = false;
                                if(result.data.msg === "account name already used") {
                                    this.errorHandler.errors.push("*This account name is already registered with another account.");
                                }
                                else if(result.data.msg === "e-mail address already used") {
                                    this.errorHandler.errors.push("*This email address is already registered with another account.");
                                }
                                else if(result.data.msg === "account name already used; e-mail address already used"){
                                    this.errorHandler.errors.push("*This account name is already registered with another account.");
                                    this.errorHandler.errors.push("*This email address is already registered with another account.");
                                }
                                else {
                                    this.requestHandler.registered = true;
                                }
                                console.log(result);
                            })
                .catch(error => {
                    this.loading = false;
                    console.error('There was an error!', error);
                    window.alert("error");
                });
                
            }
            else {
                this.loading = false;
            }
            e.preventDefault();
        },

        // function for form validation
        validateSignup:function(e) {
            this.errorHandler.errors = [];

            // account name
            if(!this.signupForm.acct_name) {
                this.errorHandler.errors.push("*Account name required.");
            }
            else if (!this.validateAcctName(this.signupForm.acct_name)) {
                this.errorHandler.errors.push('*Account name must be at least 5 characters in length.');
            }

            // email
            if(!this.signupForm.email) {
                this.errorHandler.errors.push("*Email required.");
            }
            else if(!this.validateEmail(this.signupForm.email)) {
                this.errorHandler.errors.push('*Valid email required.');
            }

            // first name 
            if(!this.signupForm.first) {
                this.errorHandler.errors.push("*First name required.");
            }

            // last name
            if(!this.signupForm.last) {
                this.errorHandler.errors.push("*Last name required.");

            }

            // phone
            if(!this.signupForm.phone) {
                this.errorHandler.errors.push("*Phone number required.");
            }
            else if(!this.validatePhone(this.signupForm.phone)) {
                this.errorHandler.errors.push("*Invalid phone number: Must be of form XXX-XXX-XXXX.");
            }

            // password
            // first check if either or both fields weren't filled in
            if(!this.signupForm.passwd || !this.errorHandler.confirmPassword) {
                if(!this.signupForm.passwd) {
                    this.errorHandler.errors.push("*Password required.");
                }
                if(!this.errorHandler.confirmPassword) {
                    this.errorHandler.errors.push("*You must confirm your password.");
                }
            }
            // if both were filled in, check if they match. if they do, check if they follow password rules   
            else if(this.signupForm.passwd && this.errorHandler.confirmPassword) {
                if (!this.equalPassword(this.signupForm.passwd, this.errorHandler.confirmPassword)) {
                    this.errorHandler.errors.push("*Passwords do not match.");
                }
                else if(!this.validatePassword(this.signupForm.passwd)) {
                    this.errorHandler.errors.push("*Password must contain at least 12 characters, and must consist of letters, numbers, or special characters.");
                    
                }
            }
            e.preventDefault()      

            // error handler for validation
            if(this.errorHandler.errors.length) {
                return false;
            }
            return true;
        },

        // helper functions for validation start here
        validateAcctName:function(acct_name) {
            if(acct_name.length < 5) {
                return false;
            } 
            return true;
        },

        validateEmail:function(email) {
            var regex = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
            return regex.test(email);
        },

        validatePhone:function(phone) {
            var regex= /^(1-)?\d{3}-\d{3}-\d{4}$/;
            return regex.test(phone);
        },

        validatePassword:function(pass) {
            var regex= /^[a-zA-Z0-9!@#$&()`.+,/"-]{12,}$/;
            return regex.test(pass);  
        },

        equalPassword:function(pass1, pass2) {
            return pass1 === pass2;
        }
        // helper functions for validation end here
    }
}
</script>