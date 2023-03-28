<template>
    <main class="text-center">
    <form @submit.prevent="submit" class="form-signin">
     <input v-model="data.email" type="email" class="form-control" placeholder="Email address" required autofocus>
      <input v-model="data.password" type="password" id="inputPassword" class="form-control" placeholder="Password" required>
      <button class="btn btn-lg btn-primary btn-block" type="submit">Sign in</button>
    </form>
  </main> 
</template>

<script lang="ts">
import {reactive} from 'vue'
import { useRouter } from 'vue-router'

    export default {
        name: "login",
        setup() {
            const data = reactive({
                name: '',
                email: '',
                password: ''
            })
            const router = useRouter()
            const submit = async () => {
                await fetch('http://localhost:3000/api/contacts/login', {
                    method: 'POST',
                    headers: {"Content-Type": "application/json"},
                    credentials: 'include',
                    body: JSON.stringify(data)
                })
                await router.push('/')
            }
            return {
                data,
                submit
            }
        }
    }
</script>

<style>
body {
  display: -ms-flexbox;
  display: -webkit-box;
  display: flex;
  -ms-flex-align: center;
  -ms-flex-pack: center;
  -webkit-box-align: center;
  align-items: center;
  -webkit-box-pack: center;
  justify-content: center;
  padding-top: 40px;
  padding-bottom: 40px;
  background-color: #f5f5f5;
}

.form-signin {
  width: 100%;
  max-width: 330px;
  padding: 15px;
  margin: 0 auto;
}
.form-signin .checkbox {
  font-weight: 400;
}
.form-signin .form-control {
  position: relative;
  box-sizing: border-box;
  height: auto;
  padding: 10px;
  font-size: 16px;
}
.form-signin .form-control:focus {
  z-index: 2;
}
.form-signin input[type="email"] {
  margin-bottom: -1px;
  border-bottom-right-radius: 0;
  border-bottom-left-radius: 0;
}
.form-signin input[type="password"] {
  margin-bottom: 10px;
  border-top-left-radius: 0;
  border-top-right-radius: 0;
}
</style>