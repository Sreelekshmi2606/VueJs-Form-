<template>
    <div class="box">
        <div class="left">
        </div>
        <div class="right">
            <form id="sign-up" @submit.prevent="submitForm">
                <div class="text-inp">
                    <input type="text" class="text-inputs" placeholder="Enter Your Name" v-model="name" />
                    <span v-if="!$v.name.required && $v.name.$dirty" class="text-danger">Name is required!</span>
                    <span v-if="!$v.name.alpha && $v.name.$dirty" class="text-danger">Name is required!</span>
                    <input type="email" class="text-inputs" placeholder="Enter Your Email" v-model="email" />
                    <span v-if="(!$v.email.required || !$v.email.email) && $v.email.$dirty" class="text-danger">Valid Email is required!</span>
                    <input type="tel" class="text-inputs" placeholder="Enter Your Phone Number" v-model="phone" />
                    <span v-if="(!$v.phone.required && $v.name.$dirty)" class="text-danger">Phone number is required</span>
                    <span v-if="(!$v.phone.minLength && $v.name.$dirty)" class="text-danger">Phone number must be a 10 digit number</span>
                    <input type="password" class="text-inputs" placeholder="Enter Your Password" v-model="password" />
                    <span v-if="!$v.password.required && $v.password.$dirty" class="text-danger">Password is required!</span>
                    <span v-if="(!$v.password.minLength || !$v.password.maxLength) && $v.password.$dirty" class="text-danger">Password must be between {{ $v.password.$params.minLength.min}} and {{ $v.password.$params.maxLength.max}} characters!</span>
                    <input type="password" class="text-inputs" placeholder="Confirm Your Password" v-model="confirm_password" />
                </div>
                <div class="some-class" id="radio-elements">
                    <label class="lab" >Gender</label>
                    <input type="radio" class="radio" name="x" value="y" id="y" v-model="gender"/>
                    <label class="lab" for="y">Male</label>
                    <input type="radio" class="radio" name="x" value="z" id="z" v-model="gender" />
                    <label class="lab" for="z">Female</label>
                    <span v-if="!$v.gender.required && $v.gender.$dirty" class="text-danger">Gender is required!</span>

                </div>

                <div class="some-class" id='t-c'>
                    <label>
                        <input type="checkbox" name="item" v-model="terms" />
                        <span class="text-check">I Agree to the terms and conditions</span>
                        <!-- <span v-if="!$v.terms.required && $v.terms.$dirty" class="text-danger">Required!</span> -->

                    </label>
                </div>
                <br>
                <button class="button" @click="submitForm">Register</button>
            </form>
        </div>
    </div>

</template>

<script>
import {
    required,
    minLength,
    maxLength,
    alpha,
    email
} from "vuelidate/lib/validators";

export default {
    name: "LoGin",
    data: () => ({
        name: "",
        email: "",
        phone: "",
        password: "",
        confirm_password: "",
        gender: ['male', 'female'],
        terms: ""
    }),
    validations: {
        name: {
            required,
            alpha
        },
        email: {
            required,
            email
        },
        phone: {
            required,
            minLength: minLength(10)
        },
        password: {
            required,
            maxLength: maxLength(12),
            minLength: minLength(6)
        },
        confirm_password: {
            required,
            maxLength: maxLength(12),
            minLength: minLength(6)
        },
        gender: {
            required
        }
    },
    methods: {
        submitForm() {
            this.$v.$touch();

            if (!this.$v.$invalid) {
                console.log(
                    `Name: ${this.name}, Email: ${this.email}, Phone: ${this.phone} ,Password: ${this.password},ConPassword: ${this.confirm_password}, Gender: ${this.gender}. Terms: ${this.terms}`
                );
            }
        }
    }




}
</script>

<style scoped>
body {
    background-image: linear-gradient(135deg, #FAB2FF 10%, #1904E5 100%);
    background-size: cover;
    background-repeat: no-repeat;
    background-attachment: fixed;
    font-family: "Open Sans", sans-serif;
    color: #333333;
}

.box {
    margin: 83px auto;
    width: 80%;
    background: #FFFFFF;
    border-radius: 10px;
    overflow: hidden;
    display: flex;
    flex: 1 1 100%;
    align-items: stretch;
    justify-content: space-between;
    box-shadow: 0 0 20px 6px #090b6f85;
}

.left {
    color: #FFFFFF;
    background-size: cover;
    background-repeat: no-repeat;
    background-image: url("https://www.mhpcolorado.org/wp-content/uploads/2020/01/bigstock-Abstract-blue-background-wal-6002095.jpg");
    background-position: center;
    overflow: hidden;
    width: 178%;
}

.box .right .text-inp input {
    width: 100%;
    padding: 10px;
    margin-top: 25px;
    font-size: 16px;
    border: none;
    outline: none;
    border-bottom: 2px solid #B0B3B9;
}

.box .right {
    padding: 50px;
    overflow: hidden;
}

.lab {
    float: left;
    clear: none;
    display: block;
    padding: 0px 1em 0px 8px;
}

.radio {
    float: left;
    clear: none;
}

.some-class {
    float: left;
}

.button {
    float: right;
    color: #fff;
    font-size: 16px;
    padding: 12px 35px;
    border-radius: 50px;
    display: inline-block;
    border: 0;
    outline: 0;
    box-shadow: 0px 4px 20px 0px #49c628a6;
    background-image: linear-gradient(135deg, #70F570 10%, #49C628 100%);
    margin-top: 15px;
}

#radio-elements {
    margin-top: 20px;
}

#t-c {
    margin-top: 17px;
}
.text-danger {
    color: red;
    font-size: 12px;
    float: left;
    padding-left: 2px;
}
</style>