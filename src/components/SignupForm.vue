<template>

<form @submit.prevent="handleSubmit">
  <label >Email:</label>
  <input type="email" required v-model="email">

  <label >Password:</label>
  <input type="password" required v-model="password">

  <div v-if="passwordError.length" class="error">{{  passwordError }}</div>


<!-- Select -->
<label >Role:</label>
<select v-model="role">
    <option value="developer">Web Developer</option>
    <option value="designer">Web Designer</option>
</select>



<!-- CheckBox -->
 <div class="terms">
    <input type="checkbox" v-model="terms" required>
    <label >Accept terms and conditions</label>

 </div>



<!-- CheckBox with Array -->
 <div>
    <input type="checkbox" value="shaun" v-model="names">
    <label >Shaun</label>
 </div>
 <div>
    <input type="checkbox" value="yoshi" v-model="names">
    <label >Yoshi</label>
 </div>
 <div>
    <input type="checkbox" value="mario" v-model="names">
    <label >Mario</label>
 </div>


 

 <!-- Adding the kills in Array as we type //press  ,+alt -->
<label >Skills:</label>
<input type="text" v-model="tempSkill" @keyup.alt="addSkill">

    <div v-for="skill in skills" :key="skill" class="pill" >
     <span @click="deleteSkill(skill)"> {{ skill }}</span>  
    </div>
 

 <div class="submit">
    <button>create account</button>    
</div>
  </form>




<!-- To show 2-way binding -->
  <p>Email: {{ email }}</p>
  <p>Password: {{ password }}</p>
  <p>Role: {{ role }}</p>
  <p>Terms accepted: {{ terms }}</p>
  <p>Names: {{ names }}</p>


 
</template>



<script>
export default {
    data(){
        return{
            email:'email address',
            password:'*****',
            role:'designer',
            terms: false,
            names: [],
            tempSkill: '',
            skills: [],
            passwordError: ''

        }
    },
    methods:{
       addSkill(e){
        if(e.key === ',' && this.tempSkill){
            if(!this.skills.includes(this.tempSkill))
            {
                this.skills.push(this.tempSkill)
            }
            
            this.tempSkill=''
        }
        
       },
       deleteSkill(skill){
        this.skills = this.skills.filter((item) => {
            if(skill !== item )
            {
                return skill
            }
           
            // if the item is not equal then it will be shown in the span... else not
            // filtter() method cycles though the array and fires a function for each item
        })
       },
       handleSubmit(){
        this.passwordError = this.password.length > 5 ? '' : 'Password must be at least 6 character long'
       }
    }
}
</script>






<style>

form{
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

input,select{
    display: block;
    padding: 10px 6px;
    width: 100%;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid #ddd;
    color: #555;
}

input[type="checkbox"]{
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
    cursor: pointer;
}

button
{
    background: rgb(56, 56, 216);
    border: 0;
    padding: 10px 20px;
    margin-top: 20px;
    color: white;
    border-radius: 20px ;
}
.submit{
    text-align: center;
}

.error{
    color: red;
    margin-top: 10px;
    font-size: 0.8em;
    font-weight: bold;
}
</style>