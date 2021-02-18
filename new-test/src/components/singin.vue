<template>
    <div class="loop">
      
       <div class="conteiner">
            <form class="singin_form" @submit.prevent="chekForm">
                <div class="singin_form_header">
                    <img src="@/assets/logo.png" alt="" class="logo_singin logo">
                </div>
                <div class="singin_form_content">
                    <input type="email" 
                    class="form_input " 
                    placeholder="Логин" 
                    id="login"
                    v-model.trim="form.login"
                    :class=" { form_invalid: ($v.form.login.$dirty && !$v.form.login.required )  }  "
                    >
                    <p class="warn_invalid login_p"
                    :class=" {invalid_text: ($v.form.login.$error) } "
                     > Поле не должно быть пустым! </p>
                    <input type="password" class="form_input" 
                    placeholder="Пароль"
                    v-model.trim="form.password"
                    :class=" { form_invalid: ($v.form.password.$dirty && !$v.form.password.required )  }  "
                    >
                    <p class="warn_invalid"
                    :class=" {invalid_text: ($v.form.password.$error) } "
                    > Поле обязательно для заполнения! </p>
                    <p class="warn_invalid_pass"
                    :class=" {invalid_text: ($v.form.password.$error) } "
                    > Пароль должен быть более 5 символов</p>
                    
                    <button to="/personal" 
                    class="btn singin_btn" 
                    type="submit"
                    @click="go_to"
                    >Войти</button>
                    
                </div>
            </form>
        </div>


    </div>
</template>



<script>
import { required, minLength, email } from 'vuelidate/lib/validators'



export default {
    name: 'singin',
    path: '/singin',
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
            login: { required  , email } ,
            password: { required ,minLength : minLength(5)} ,
        }
        
    },
    
    methods: {
        chekForm() {
            if(this.$v.$invalid) {
                this.$v.$touch()
                return
            }
         }
    },

    

    
}
</script>


<style>
*{
    font-size: 14px;
    font-family: 'Montserrat', sans-serif;
    font-weight: 500;
    outline: none;
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
body {
    margin: 0;
    padding: 0;
    background: #fff;
    line-height: 20px;  
}

a {
    text-decoration: none;
    color: inherit;
}

li {
    list-style-type: none;
}

.flex_helper {
    display: flex;
}

.header {
    height: 64px;
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

.logo {
    width: 130px;
    height: 30px;
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

.btn--sm {
    width: 200px;
}

.sidebar {
    display: block;
    width: 200px;

    background: #fff;

    padding: 40px 0;
    box-sizing: border-box;

    

}

.sidebar_inner {
    display: block;
}

.logo_profile {
    margin-bottom: 30px;
}

.sidebar_item a {
    display: flex;
}

.sidebar_item a p {
    transform: translateY(-10px);
}

.sidebar_nav_icon {
    width: 20px;
    height: 20px;
    margin-right: 8px;
}

.content_profile {
    display: block;
    max-width: 1080px;
    min-height: 100vh;
    background: #EFF1F9;

    padding: 50px;
    box-sizing: border-box;
}

.profile_form {
    display: block;

    background: #fff;
    border-radius: 10px;
    box-sizing: border-box;
    padding: 40px;
}

.flex_inner {
    box-sizing: border-box;
    width: 50%;
    
}

.flex_left {
    margin-right: 80px;
}

.title {
    font-size: 20px;
    font-weight: 500;
    color: #303136;
    margin-bottom: 48px;
}

.profile_input {
    width: 100%;
    background: none;
    border: none;
    border-bottom: 1px solid #6F849C;
    color: #303136;
    margin-top: 32px;
    margin-bottom: 24px;
}

.profile_label {
   color: #6F849C; 
   font-weight: 400;
}

.profile_save {
    display: block;
    margin-left: auto;
}

.header {
    display: none;
}

.logo_header_mobile {
    display: block;
    margin: 5px auto;
}



.burger_menu::after,
.burger_menu::before {
    content: "";
    display: block;
    position: absolute;
    top: 20px;
    left: 20px;
    width: 20px;
    height: 2px;
    background: #BD0D22;
    transition: .3s;
}
.burger_menu::after {
    top: 15px;
}

.burger_list {
    display: none;
    position: fixed;

    width: 100%;
    height: 100%;

    left: 0;
    top: 0;
    z-index: 300;
    background: #fff;
    margin-top: 64px;

    transform: translateX(-400px);
    transition: translate .5s;
}

.burger_list_active {
    transform: translateX(0);
}

@media (max-width: 800px) {
    .flex_helper {
        display: block;
        width: 100%;
    }

    .sidebar {
        display: none;
    }

    .header {
        display: flex;
    }
    .content_profile {
        padding: 40px 17px;
        box-sizing: border-box;
    }
    .flex_inner {
        width: 100%;
    }
    
    
    
}
</style>