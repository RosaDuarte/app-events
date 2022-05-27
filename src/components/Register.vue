<template>
    <div class="box">
        <h2 class="subtitle is-4 has-text-centered">Registro</h2>
        <div>
            <div class="field">
                <p v-if="errors.length" class="mb-2">
                    <b>Por favor, corrija el siguiente error:</b>
                    <ul class="mb-2">
                        <li v-for="error in errors" :key="error.id" class="has-text-centered">{{ error }}</li>
                    </ul>
                </p>
                <p class="control has-icons-left has-icons-right">
                    <input class="input" type="email" placeholder="Email" v-model="email" name="email">
                    <span class="icon is-small is-left">
                        <i class="fas fa-envelope"></i>
                    </span>
                </p>
            </div>
            <div class="field">
                <p class="control has-icons-left">
                    <input class="input" type="password" placeholder="Password" v-model="password" name="password">
                    <span class="icon is-small is-left">
                        <i class="fas fa-lock"></i>
                    </span>
                </p>
            </div>
            <div class="field has-text-centered">
                <p class="control">
                    <button class="button" @click="saveRecord">
                        Registrarse
                    </button>
                </p>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data(){
        return{
            register: [],
            errors: [],
            email: "",
            password: ""
        }
    },
    
    methods:{
        saveRecord(){
            this.checkForm();
            let person = {email: this.email, password: this.password}
            this.register.push(person);

            this.email = "";
            this.password = "";

            this.records();
            
        },
        checkForm(e) {
            this.errors = [];
            if (!this.email) {
                this.errors.push('El correo electrónico es obligatorio.');
            } else if (!this.validEmail(this.email)) {
                this.errors.push('El correo electrónico debe ser válido.');
            }

            if(!this.validPassword(this.password)){
                this.errors.push('La contraseña debe contener entre 4 y 12 dígitos.');
            }

            if (!this.errors.length) {
                return true;
            }

            e.preventDefault();
        },
        validEmail(email) {
            const re = /^[a-zA-Z0-9_.+-]+@[a-zA-Z0-9-]+\.[a-zA-Z0-9-.]+$/;
            
            return re.test(email);
        },
        validPassword(password) {
            const re = /^.{4,12}$/; // 4 a 12 digitos.	
            
            return re.test(password);
        },
        records(){
            const parsed = JSON.stringify(this.register);
            localStorage.setItem('register', parsed);
        }
    },
    mounted(){
    if(localStorage.getItem('register')){
      try{
        this.register = JSON.parse(localStorage.getItem('register'));
      }catch(e){
        localStorage.removeItem('register')
      }
    }
  },
}
</script>

<style scoped>
    .box{
        width: 300px;
        height: auto;
        background-color: var(--gray);
    }
    h2{
        color: var(--text);
        font-weight: 700;
    }
    b{
        color: #c82121;
    }
    li{
        color: var(--text);
    }
    input::placeholder{
        color: #929aab;
    }
    i{
        color: var(--blue-light);
    }
    button{
        background-color: transparent;
        border: 2px solid var(--blue);
        border-radius: 100px;
        font-family: 'Roboto', sans-serif;
        font-weight: 700;
        color: var(--text);
    }
    button:hover{
        color: var(--white);
        background: var(--highlight);
        transition: background 1s;
    }
    .button:focus:not(:active){
        background: transparent;
        color: var(--blue-light);
        box-shadow: none;
        border: 2px solid var(--white);
    }
</style>