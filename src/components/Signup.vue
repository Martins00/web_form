<template>
  <h1>ESCAPE PLAN</h1>
  <h5>Make sure your details are correct</h5>

  <form @submit.prevent="handleSubmit">
    <label>E-MAIL:</label>
    <input type="email" required v-model="email">

    <label>PASSWORD:</label>
    <input type="password" required v-model="password">
    <p v-if="passwordError" class="error">{{passwordError}}</p>

    <label>ROLE:</label>
    <select v-model="role">
      <option value="developer">Web Developer</option>
      <option value="designer">Product Designer</option>
      <option value="data">Data Analyst</option>
      <option value="manager">Product Manager</option>
    </select>

    <div>
      <input type="checkbox" v-model="terms">
      <label>Terms and Conditions</label>
    </div>

    <label>Skillset:</label>
    <input type="text" v-model="tempSkill" @keyup.alt="addSkill">
    <div v-for="skill in skills" :key="skill" class="pill" >
      <span @click="deleteSkill(skill)">{{ skill }}</span>  
    </div>

    <div class="submit">
      <button class="submit">
        Submit Application
      </button>
    </div>

  </form>
  <!-- <p>mail: {{email}}</p>
  <p>password: {{password}}</p>
  <p>role: {{role}}</p>
  <p>terms: {{terms}}</p>
  <p>skills: {{skills}}</p> -->
</template>

<script>
export default {
  data() {
    return {
      email: '',
      password: '',
      role: '',
      terms: false,
      tempSkill: '',
      skills: [],
      passwordError: ''
    }
  },
  methods: {
    addSkill(e) {
      if(e.key === ',' && this.tempSkill) {
        if(!this.skills.includes(this.tempSkill)) {
          this.skills.push(this.tempSkill)
        }   
          this.tempSkill = ''
      } 
    },
    deleteSkill (skill) {
      this.skills = this.skills.filter((item) => {
        return skill !== item 
      })
    },
    handleSubmit() {
      this.passwordError = this.password.length > 5?
      '' : 'Password must be at least 6 characters'
      if (!this.passwordError) {
        console.log(this.email)
        console.log(this.password)
        console.log(this.role)
        console.log(this.skills)
      }
    }  
  }
} 
</script>

<style>
h1, h5{
  color: #aaa;
}
  form{
    max-width: 420px;
    margin: 30px auto;
    background: white;
    text-align: left;
    padding: 40px;
    border-radius: 10px;
  }
  label{
    color: #aaa;
    display: inline-block;
    margin: 25px 0 15px;
    font-size: 0.6rem;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
  }
  input, select{
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
    background: aqua;
    border: 0;
    padding: 10px 20px;
    margin-top: 20px;
    color: white;
    border-radius: 20px;
    cursor: pointer;
  }
  .submit{
    text-align: center;
  }
  .error{
    color: red;
    margin-top: 10px;
    font-size: 0.8rem;
    font-weight: bold;
  }
</style>