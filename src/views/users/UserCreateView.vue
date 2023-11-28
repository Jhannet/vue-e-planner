<script>
import axios from "axios";

export default {
    name: "UserCreateView",
    data() {
        return {
            errors: [],
            model: {
                user: {
                    username: '',
                    password: '',
                    email: '',
                    createdAt: '',
                    userDetail: {
                        firstName: '',
                        lastName: '',
                        age: '',
                        birthDay: ''
                    }
                }
            }
        }
    },
    methods: {
        saveUser() {
            axios.post('http://localhost:8081/v1/users', this.model.user)
                .then(res => {
                    alert('User was saved successful');
                    this.model.user = {
                        username: '',
                        password: '',
                        email: '',
                        createdAt: '',
                        userDetail: {
                            firstName: '',
                            lastName: '',
                            age: '',
                            birthDay: ''
                        }
                    }
                }).catch(function (error) {
                    // hangle error on UI site
                })
        },
        checkForm: function (e) {
            e.preventDefault();

            this.errors = [];

            if (!this.model.user.username.length) {
                this.errors.push('Username is required.');
            }
            if (!this.model.user.password.length) {
                this.errors.push('Password is required.');
            }
            if (!this.model.user.email.length) {
                this.errors.push('Email is required.');
            }
            if (!this.model.user.userDetail.firstName.length) {
                this.errors.push('First name is required.');
            }
            if (!this.model.user.userDetail.lastName.length) {
                this.errors.push('Last name is required.');
            }

            if (!this.errors.length) {
                this.saveUser();
                return true;
            }

        }
    }
}
</script>

<template>
    <div class="container mt-5">
        <div class="card">
            <div class="card-header">
                <h4>Add User</h4>
            </div>
            <div class="card-body">
                <form @submit="checkForm">
                    <p v-if="errors.length">
                        <b>Please fix the following errors:</b>
                    <ul>
                        <li v-for="error in errors">{{ error }}</li>
                    </ul>
                    </p>
                    <div class="mb-3">
                        <label for="username">Username</label>
                        <input type="text" v-model="model.user.username" name="username" id="username" class="form-control">
                    </div>
                    <div class="mb-3">
                        <label for="password">Password</label>
                        <input type="password" v-model="model.user.password" name="username" id="password" class="form-control">
                    </div>
                    <div class="mb-3">
                        <label for="email">Email</label>
                        <input type="email" v-model="model.user.email" name="email" id="email" class="form-control">
                    </div>
                    <div class="mb-3">
                        <label for="firstName">First Name</label>
                        <input type="text" v-model="model.user.userDetail.firstName" name="firstName" id="firstName" class="form-control">
                    </div>
                    <div class="mb-3">
                        <label for="lastName">Last Name</label>
                        <input type="text" v-model="model.user.userDetail.lastName" name="lastName" id="lastName" class="form-control">
                    </div>
                    <div class="mb-3">
                        <label for="age">Age</label>
                        <input type="number" v-model="model.user.userDetail.age" name="age" id="age" class="form-control">
                    </div>
                    <div class="mb-3">
                        <label for="birthDay">Birth Day</label>
                        <input type="text" v-model="model.user.userDetail.birthDay" name="birthDay" id="birthDay" class="form-control">
                    </div>
                    <div class="mb-3">
                        <button type="submit" class="btn btn-primary">
                            Save
                        </button>&nbsp;
                        <RouterLink to="/users" class="btn btn-primary">
                            Back
                        </RouterLink>
                    </div>
                </form>
            </div>
        </div>
    </div>
</template>

<style scoped></style>