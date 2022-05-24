<template>
  <main>
    <header>
      <img class="manflixLogo" src="@/static/manflix.png" alt="Manflix"/>
    </header>

    <div class="loginContainer manflix-flexcolumn">
      <!-- QUANDO DOU UM SUBMIT A PAGINA REGARREGA! Para evitar isso, usamos .prevent -->
      <form v-on:submit.prevent="makeLogin()" class="login pl-4 pr-4 w-8 md:w-3">
        <!-- w8 está ate o maximo de sm! passou do sm, é w-4 -->
        <h2 class="mb-3 sm:mb-4">Sign In</h2>
        <input type="email" 
        class="loginField w-full pl-3 mb-3 h-3rem" required 
        placeholder="Email ou número de telefone" v-model="user.username" v-on:change="()=>{this.message = ''}"/> 
        <Password v-model="user.password" required
        placeholder="Password"
        :feedback="false"
        toggleMask
        inputClass="loginField w-full pl-3 h-3rem primeFieldReset primeFieldPassword"
        />
        <!-- mb eh margin bottom -->
        <!--pl padding left -->
        <!-- h -->
        <!-- margin: externo -->
        <!-- padding: interno -->
        <p class="errorMessage"> {{message}}</p>
        <Toast/>
        <button
        class="loginField buttonLogin mb-2 mt-5 h-3rem sm:3rem"
        >Sign In
        </button>
        <div class="remember manflix-flexrow justify-content-between">
          <label><input type="checkbox" checked>Remember me</label>
          <a href="#">Need help?</a>

        </div>
      </form>
    </div>

    <footer>
    </footer>
    
  </main>
</template>

<script>
export default {
  name: 'login',
  data(){
    return{
      user: {
        username: "",
        password: ""
      },
      message: ""
    }
  },
  methods: {
    makeLogin: async function(){
      this.$auth.loginWith(
        "local", {data: this.user}
      ).then((response)=>{
        console.log("Usuario logado!");
      }).catch((response)=>{
        console.log(response);
        this.user.username = "";
        this.user.password = "";
        this.message = "User or Password is wrong!"
        setTimeout(()=>{
          this.message = '';
        }, 5000)

        this.$toast.add(
          {
            severity: "error",
            summary: 'Error to connect',
            detail:'User or Password is wrong',
            life: 5000
          }
        )
      })
      // auth eh um pacote para autenticacao dentro do vue! De forma facil e automática. É um plugin
    }
  }
}
</script>

<style lang="scss" scoped>
$header-height: 10vh;
$footer-height: 16vh;

main{
  width: 100vw;
  height: 100vh;
  max-height: 100vh;
  max-width: 100vw;

  background-image: url("@/static/login_background.jpg");
  background-repeat: no-repeat;
  background-position: center;
  background-size: cover;

  header{
    width: 100vw;
    height: $header-height;
    min-height: 60px;
    /* background-color: red; */

    .manflixLogo{
      height: 85%;
      width: 250px;
      margin-left: 10px;
      margin-top: 10px;
    }
  }

  .loginContainer{
    width: 100vw;
    height: calc(100vh - $footer-height - $header-height);

    .login{
      display: flex;
      flex-direction: column;
      width: 25vw;
      height: 90%;
      background-color: var(--dark-transparent-color);
      color: white;
      padding-top: 35px;
      padding-bottom: 100px;
      

      .loginField{
        border: none;
        border-radius: 3px;
        color: white;
        outline: 0;
        background-color: var(--background-field-color);

        &::placeholder{
          color: var(--placeholder-field-color);
          font-size: 14px;
          font-family: 'NetflixSansRegular';
        }
      }

      .buttonLogin{
        background-color: var(--background-btn-color);
        cursor: pointer;
        font-family: 'NetflixSansBold';
      }

      .remember{
        font-size: 12px;
        color: var(--placeholder-field-color);
        input{
          margin-left: 5px;
          width:auto;
        }
        /* label{
          
        } */
        a{
          margin-right: 5px;
          width:auto;
          text-decoration: none;
          color: var(--placeholder-field-color);
        }
      }
      
    }
  }

  .errorMessage{
    color: #FF2468;
    font-size: 12px;
    width: 100%;
    text-align: center;
    margin-top: 10px;
  }

  footer{
    width: 100vw;
    height: $footer-height;
    background-color: var(--dark-transparent-color);
  }

}

/* @media screen and (max-width:1000px){
  .login{
    width: 40vw !important;
  }

}

@media screen and (max-width:450px){
  .login{
    width: 70vw !important;
  }

}*/
@media screen and (max-width:280px){
  header{
    background-color: var(--dark-transparent-color) !important;
  }
  .loginContainer{
    height:calc(100vh - $header-height) !important;
  }
  .login{
    width: 100vw !important;
    height: 100vh !important;
  }
  h2{
    color: white !important;
  }
  footer{
    display: none !important;
  }
} 

</style>
