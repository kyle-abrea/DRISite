<template>
    <div class='registration'>

        <!-- TODO:
        - mockups
        - make UI look like a actual webpage
            - add header, footer
            - reformat registration box
        - UI response if user is successful in signing in -->
        
        <body>
            <h1>Welcome to WRCC! Create an account here!</h1>
            <div id='formContainer'>
                
                <form  @submit="register"  novalidate='true'>

                    <div id='errorContainer' >
                        <p v-if='errorHandler.errors.length'>
                            <b>Please correct the following error(s):</b> 

                            <ul>   
                                <li v-for="error in errorHandler.errors" v-bind:key="error.id">{{ error }}</li>
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
                        <input v-model.trim="signupForm.first" type="text" placeholder="" id="first" style="text-transform:uppercase" />
                    </div>

                    <div id='fieldContainer'>
                        <label for="last">Last Name: </label>
                        <input v-model.trim="signupForm.last" type="text" placeholder="" id="last" style="text-transform:uppercase" />
                    </div>

                    <div id='fieldContainer'>
                        <label for="phone">Phone Number: </label>
                        <input v-model.trim="signupForm.phone" type="text" placeholder="" id="phone" />
                    </div>

                    <div id='fieldContainer'>
                        <label for="password">Password</label>
                        <input v-model.trim="signupForm.passwd" type="password" placeholder="12 or more characters, 1 or more numbers, 1 or more special characters" id="password" />
                    </div>

                    <div id='fieldContainer'>
                        <label for="password">Confirm Password: </label>
                        <input v-model.trim="errorHandler.confirmPassword" type="password" placeholder="" id="confirmPassword" />
                    </div>

                    <div id='fieldContainer'>
                        <button @click="register" class="button">Sign Up</button>
                    </div>

                </form>
            

            </div>
        </body>
    </div>
    
</template>

<script>

import axios from 'axios'
// import VueAxios from 'vue-axios'

export default {
    // e1: '#app',

    data() {
        return {
            
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
                //test password to ctrl+c & ctrl+p: 4$qwertyuiop
            },

            // performingRequest: false;

        }
    },

    methods: {
        register:function(e) {
            // window.alert("time to register");
            if(this.validateSignup(e)) {
                // window.alert("success");
                axios.post("https://wrcc.dri.edu/pass", this.signupForm, {
                            headers: { 'Content-Type': 'application/x-www-form-urlencoded' }
                            }).then((result) => { 
                    console.warn(result)
                })
                .catch(error => {
                    // element.parentElement.innerHTML = `Error: ${error.message}`;
                    console.error('There was an error!', error);
                });
            }
            // else {
            //     window.alert("fail");
            // }
            e.preventDefault();
        },

        validateSignup:function(e) {
            this.errorHandler.errors = [];

            // account name 
            if(!this.signupForm.acct_name) {
                this.errorHandler.errors.push("*Account name required.");
                // window.alert("*Account name required");
            }
            else if (!this.validateAcctName(this.signupForm.acct_name)) {
                this.errorHandler.errors.push('*Account name must be at least 5 characters in length.');
            }

            //email
            if(!this.signupForm.email) {
                this.errorHandler.errors.push("*Email required.");
                // window.alert("*Email required");
            }
            else if(!this.validateEmail(this.signupForm.email)) {
                this.errorHandler.errors.push('*Valid email required.');
            }

            // first name 
            if(!this.signupForm.first) {
                this.errorHandler.errors.push("*First name required.");
                // window.alert("*First name required");
            }

            // last name
            if(!this.signupForm.last) {
                this.errorHandler.errors.push("*Last name required.");
                // window.alert("*Last name required");
            }

            //phone
            if(!this.signupForm.phone) {
                this.errorHandler.errors.push("*Phone number required.");
                // window.alert("*Phone number required");
            }
            else if(!this.validatePhone(this.signupForm.phone)) {
                this.errorHandler.errors.push("*Invalid phone number: Must be of form XXX-XXX-XXXX.");
            }

            //password
            //first check if either or both fields weren't filled in
            if(!this.signupForm.passwd || !this.errorHandler.confirmPassword) {
                if(!this.signupForm.passwd) {
                    this.errorHandler.errors.push("*Password required.");
                    // window.alert("*Password required");
                }
                if(!this.errorHandler.confirmPassword) {
                    this.errorHandler.errors.push("*You must confirm your password.");
                    // window.alert("*You must confirm your password");
                }
            }
            // if both were filled in check if they match. if they do, check if they follow password rules   
            else if(this.signupForm.passwd && this.errorHandler.confirmPassword) {
                if (!this.equalPassword(this.signupForm.passwd, this.errorHandler.confirmPassword)) {
                    this.errorHandler.errors.push("*Passwords do not match.");
                }
                else if(!this.validatePassword(this.signupForm.passwd)) {
                    this.errorHandler.errors.push("*Password must contain at least 12 characters, at least 1 number, and at least 1 letter.");
                }
            }

            //TESTING:
            // window.alert(this.errorHandler.errors.length);s
            // window.alert(this.errorHandler.errors[0]);
            // window.alert(this.signupForm.acct_name);
            // window.alert(this.signupForm.first);
            // window.alert(this.signupForm.last);
            e.preventDefault()      


            if(this.errorHandler.errors.length) {
                return false;
            }
            return true;
        },

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

        equalPassword:function(pass1, pass2) {
            return pass1 === pass2;
        },

        validatePassword:function(pass) {
            var regex= /^(?=.*[A-Za-z])(?=.*\d)(?=.*[@$!%*#?&])[A-Za-z\d@$!%*#?&]{12,}$/;
            return regex.test(pass);
        },

     

    }
}
</script>