vue
<template>
    <form @submit.prevent="handleSubmit">
        <h3>Sign Up</h3>
        <div class="form-group">
            <label>First Name</label>
            <input type="text" class="form-control" v-model="firstName" placeholder="First Name" required />
        </div>
        <div class="form-group">
            <label>Last Name</label>
            <input type="text" class="form-control" v-model="lastName" placeholder="Last Name" required />
        </div>
        <div class="form-group">
            <label>Email</label>
            <input type="email" class="form-control" v-model="email" placeholder="Email" required />
        </div>
        <div class="form-group">
            <label>Password</label>
            <input type="password" class="form-control" v-model="password" placeholder="Password" required />
        </div>
        <div class="form-group">
            <label>Confirm Password</label>
            <input type="password" class="form-control" v-model="confirmPassword" placeholder="Confirm Password" required />
            <p v-if="passwordMismatch" style="color: red;">Passwords do not match.</p>
        </div>
        <button type="submit" :disabled="passwordMismatch">Submit</button>
    </form>
</template>

<script>
export default {
    // eslint-disable-next-line vue/multi-word-component-names
    name: 'Signup',
    data() {
        return {
            firstName: '',
            lastName: '',
            email: '',
            password: '',
            confirmPassword: ''
        };
    },
    computed: {
        passwordMismatch() {
            return this.password !== this.confirmPassword;
        }
    },
    methods: {
        handleSubmit() {
            if (this.passwordMismatch) {
                // Handle the case where passwords do not match
                alert("Passwords do not match.");
                return;
            }

            // Handle the signup logic here (e.g., API call)
            console.log('Form submitted:', {
                firstName: this.firstName,
                lastName: this.lastName,
                email: this.email,
                password: this.password
            });

            // Reset form fields after submission if needed
            this.resetForm();
        },
        resetForm() {
            this.firstName = '';
            this.lastName = '';
            this.email = '';
            this.password = '';
            this.confirmPassword = '';
        }
    }
};
</script>