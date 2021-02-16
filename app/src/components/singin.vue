<template>  
    

        <div class="conteiner">
            <form class="singin_form" @submit.prevent='chekForm'>
                <div class="singin_form_header">
                    <img src="@/assets/logo.png" alt="" class="logo_singin logo">
                </div>
                <div class="singin_form_content">
                    <input type="email" class="form_input " 
                    placeholder="Логин" 
                    id="login"
                    :class= " $v/form.login.$error ? 'warn_invalid' : ''  "
                    v-model.trim="form.login"
                    >
                    <p class="warn_invalid " v-if= " !$v.form.login.$dirty  "  > Поле обязательно для заполнения! </p>
                    <input type="password" class="form_input" 
                    placeholder="Пароль"
                    v-model.trim="form.password"
                    >
                    <p class="warn_invalid"> Поле обязательно для заполнения! </p>
                    <p class="warn_invalid_pass"> Пароль должен быть более 4 символов</p>
                    <button class="btn singin_btn">Войти</button>
                    
                </div>
            </form>
      </div>

    
</template>


<script>
import { validationMixin } from 'vuelidate'
import { required, minLength,  } from 'vuelidate/lib/validators'


export default {
    mixins: [validationMixin],
    data() {
    return {
      form: {
          login: '',
          password: '',
      }
    }
  },
    components: {
        
    },
    validations: {
        form: {
            password: {{ required,minLength(5) }}
            login: {
                { required }
            }
        }
    }
    methods: {
        chekForm() ;{
            this.$v.form.$touch()
            if (this.$v.form.$error) {
                console.log(Повезло)
            }
        }
    }

}
</script>

<style lang="scss" scoped>

*{
    font-size: 14px;
    font-family: 'Montserrat', sans-serif;
    font-weight: 500;
    outline: none;
}

body {
    margin: 0;
    padding: 0;
    background: #fff;
    line-height: 20px;  
}
.conteiner {
    display: block;
    max-width: 1280px;
    height: 100%;
    
    margin: auto;
    text-align: center;
}

.singin_form {
    display: block;
    max-width: 350px;
    padding: 0 4px;
    margin: 180px auto;

}


.form_input {
    width: 100%;
    height: 44px;

    margin: 16px 0;
    border: 1px solid #CBCBCB;
    box-sizing: border-box;
    border-radius: 10px;

    font-weight: 400;
    color: #9496A6;
    font-family: 'Montserrat', sans-serif;

}

.btn {
    width: 100%;
    height: 44px;

    border-radius: 10px;
    border: none;

    background: #D6073D;
    color: #fff;
    font-weight: 500;
}

.btn:hover {
    box-shadow: 10px  #000;
}

.logo {
    width: 130px;
    height: 30px;
}

.form_invalid {
    background: rgb(255, 105, 105);
}

.warn_invalid,
.warn_invalid_pass {
    display: none;
    color: #D6073D;
}

.invalid_text {
    display: block;
}
    
</style>