<template>
    <!-- .prevent stops the default reflashing -->
    <form @submit.prevent="handleSubmit">
        <label>Email:</label>
        <!-- email in v-model binds to the one in data() -->
        <input type="email" required v-model="email">

        <label>Password:</label>
        <input type="password" required v-model="password">
        <div v-if="passwordError" class="error">{{ passwordError }}</div>

        <label>Role:</label>
        <select v-model="role">
            <option value="developer">Web Developer</option>
            <option value="designer">Web Designer</option>
        </select>

        <label>Skills:</label>
        <!-- .alt prevents the comma to enter the array -->
        <input type="text" v-model="tempSkill" @keyup.alt="addSkill">

        <div v-for="skill in skills" :key="skill" class="pill" @click="removeSkill(skill)">
            {{ skill }}
        </div>

        <div class="terms">
            <!-- users can't process unless they fill the checkbox -->
            <input type="checkbox" v-model="terms" required>
            <label>Accept terms and conditions</label>
        </div>

        <div class="submit">
            <button>Create an Account</button>
        </div>

        <!-- the value inside <input> goes to the names array in data() if checked -->
        <!-- <div>
            <input type="checkbox" value="shaun" v-model="names">
            <label>Shaun</label>
        </div>
        <div>
            <input type="checkbox" value="yoshi" v-model="names">
            <label>yoshi</label>
        </div>
        <div>
            <input type="checkbox" value="mario" v-model="names">
            <label>mario</label>
        </div> -->

    </form>

    <p>Email: {{ email }}</p>
    <p> Password: {{ password }}</p>
    <p>Role: {{ role }}</p>
    <p>Terms accepted: {{ terms }}</p>
    <!-- <p>Names: {{ names }}</p> -->
</template>

<script>
export default {
    data() {
        return {
            email: '',
            password: '',
            // role will store the vaule in <option>
            role: '',
            terms: false,
            // names: []
            tempSkill: '',
            skills: [],
            passwordError: ''
        }
    },
    methods: {
        addSkill(e) {
            // when user has entered a skill already and enters comma 
            if ( e.key === ',' && this.tempSkill) {
                // this if statement eliminates duplicate
                if (!this.skills.includes(this.tempSkill)) {
                    this.skills.push(this.tempSkill);
                }
                this.tempSkill = '';
            }
        },
        removeSkill(skill) {
            const index = this.skills.indexOf(skill);
            this.skills.splice(index, 1);

            // alternative solution

            // this.skills = this.skills.filter((item) => {
            //     return skill != item;
            // });
        },
        handleSubmit() {
            // validate password
            this.passwordError = this.password.length > 5 ? '' : 'Password must be at least 6 chars long';
        
            if (!this.passwordError) {
                console.log('email: ', this.email);
            }
        }
    }
}
</script>

<style>
form {
    max-width: 420px;
    margin: 30px auto;
    background: white;
    text-align: left;
    padding: 40px;
    border-radius: 10px;
}
label {
    color: #aaa;
    display: inline-block;
    margin: 25px 0 15px;
    font-size: 0.6em;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
}
input, select {
    display: block;
    padding: 10px 6px;
    width: 100%;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid #ddd;
    color: #555;
}
input[type="checkbox"] {
    display: inline-block;
    width: 16px;
    margin: 0 10px 0 0;
    position: relative;
    top: 2px;
}
.pill {
    display: inline-block;
    margin: 20px 10px 0 0;
    padding: 6px 12px;
    background: #eee;
    border-radius: 20px;
    font-size: 12px;
    letter-spacing: 1px;
    font-weight: bold;
    color: #777;
    cursor: pointer;
}
button {
    background: #0b6dff;
    border: 0;
    padding: 10px 20px;
    margin-top: 20px;
    color: white;
    border-radius: 20px;
}
.submit {
    text-align: center;
}
.error {
    color: #ff0062;
    margin-top: 10px;
    font-size: 0.8em;
    font-weight: bold;
}
</style>