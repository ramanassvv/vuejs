<template>
    <form>
        <label>Email</label>
        <input type="email" required v-model="email"/>

        <label>Password</label>
        <input type="password" required v-model="password" />

        <label>Role: </label>
        <select v-model="role"> 
            <option value="" selected disabled>Select</option>
            <option v-for="role in roleItems" :value="role.title" :key="role.id">{{role.title}}</option>    
        </select> 

        <label>Skills</label>
        <input type="text" v-model="tempskill" @keyup.alt="addSkills"/>
        <div v-for="skill in skills" :key="skill" class="pill">
            <span @click="deleteSkill(skill)">{{skill}}</span>
        </div>

        <div class="terms"> 
            <input type="checkbox" v-model="terms" required>
            <label> Accept terms and Conditions </label>   
        </div>   

        <div class="submit">
            <button> Create an Account </button>
        </div>
    </form>
</template>

<script>
export default {
    name: 'InputForm',
    data(){
        return {
            email: '',
            password: '',
            roleItems: [ 
                {title: 'Web Designer', id: 1}, 
                {title: "Web Developer", id: 2},
                {title: "UI Developer", id: 3},
                {title: "UX Designer", id: 4}
            ],
            role: '',
            terms: false,
            tempskill:'',
            skills: []
        }
    },
    methods : {   
        addSkills(e){
          if(e.key === ',' && this.tempskill) {
            if(!this.skills.includes(this.tempskill)) {
                this.skills.push(this.tempskill);
            }
            this.tempskill = ''
            }
        }, 
        
        deleteSkill(skill) {
            this.skills =this.skills.filter((item) =>  {
                return skill !== item;
            })
        }
    }
}
</script>
<style>
    form {
        max-width: 420px;
        margin: 30px auto;
        background-color: white;
        text-align: left;
        padding: 40px;
        border-radius: 10px;
    }
    label {
        color: #aaaa;
        display: inline-block;
        margin: 23px 0 15px;
        font-size: 1em;
        letter-spacing: 1px;
        font-weight: bold;
    }

    input, select{
        display: block;
        padding: 10px 6px;
        width: 100%;
        box-sizing: border-box;
        border: none;
        border-bottom: 1px solid #dddd;
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
        background: #eee;
        margin: 20px 10px 0 0;
        padding: 6px 12px;
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
</style>