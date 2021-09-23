<template>
  <form @submit.prevent="handleSubmit">
    <label>Email:</label>
    <input type="email" required v-model="email">

    <label>Password:</label>
    <input type="password" required v-model="password">
    <div v-if="passwordError" class="error"> {{ passwordError }}</div>

    <label >Role: </label>
    <select v-model="role"> 
        <option value="developer"> Web Developer</option>
        <option value="designer"> Web Designer</option>
    </select>

    <label>Skills:</label>
    <input type="text" v-model="tempSkill" @keyup.alt="addSkill">
    <div v-for="skill in skills" :key="skill" class="pill" @click="deleteSkill(skill)">
        {{ skill }}
    </div>
    
    <div class="terms">
      <input type="checkbox" v-model="terms" required>
      <label>Accept terms and conditions</label>
    </div>

    <div class="submit">
        <button>Create an Account</button>
    </div>

  </form>

</template>

<script>
export default {
    data(){
        return{
            email:'',
            password: '',
            role:'developer',
            terms:false, 
            tempSkill: '', // Empty srting -> Stores a temporary skill 
            skills: [], // Empty array -> Stores all skills the user inputs 
            filtered:[],
            passwordError: ''
        }
    },
    
    methods:{
        addSkill(e){
            console.log(e)
            if (e.key === ',' && this.tempSkill){
                if (!this.skills.includes(this.tempSkill)){
                    this.skills.push(this.tempSkill)
                }
                else {
                    alert("This skill has already been added!")
                }
                this.tempSkill='' 
            }         
        },
        deleteSkill(skill){
            console.log(`clicked on ${skill}`)
            this.filtered = this.skills.filter( (elem) => elem!=skill)
            this.skills = this.filtered
            console.log (this.filtered)
        },
        handleSubmit (){
            //console.log("form submitted")
            this.passwordError = this.password.length > 5 ? '' : 'Password must be at least 6 chars long'

            if (!this.passwordError){
                console.log('email: ', this.email)
                console.log('password: ', this.password)
                console.log('role: ', this.role)
                console.log('skills: ', this.terms)
                console.log('terms accepted: ', this.terms)
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
input[type="checkbox"]{
    display: inline-block; /*Checkbox Sits next to the label*/
    width: 16px;
    margin: 0 10px 0 0; /*Margin to right*/
    position: relative;
    top: 2px;
}
.pill{
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
button{
    background: #0b6dff;
    border: 0;
    padding: 10px 20px;
    margin-top: 20px;
    color: white;
    border-radius: 20px;
}
.submit{/*aligns the buttom inside the form */
    text-align: center;
}
.error{
    color:#ff0062;
    margin-top: 10px;
    font-size: 0.8em;
    font-weight: bold;
}
</style>