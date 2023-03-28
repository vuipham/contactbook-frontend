<template>
    <nav class="navbar navbar-expand navbar-dark bg-dark">
        <!-- <a href="/" class="navbar-brand">Ứng dụng Quản lý danh bạ</a> -->
        <router-link :to="{ name: 'contactbook' }" class="nav-link">
                Ung dung quan ly danh ba
                <i class="fas fa-address-book"></i>
        </router-link>
        <div class="mr-auto navbar-nav">
            <li class="nav-item">
                <router-link :to="{ name: 'contactbook' }" class="nav-link">
                Danh bạ
                <i class="fas fa-address-book"></i>
                </router-link>
            </li>
            <li class="nav-item ml-5" v-if="!auth">
                <router-link :to="{ name: 'register' }" class="nav-link">
                Dang ky
                </router-link>
                <router-link :to="{ name: 'login' }" class="nav-link">
                Dang nhap
                </router-link>
            </li>
            <li class="nav-item ml-5" v-if="auth">
                <a href="/login" class="nav-link" @click="logout">Dang xuat</a> 
            </li>
        </div>
    </nav>
</template>

<script lang="ts">
    import { computed } from 'vue';
    import Store  from '../store/index'

    export default {
        name: "AppHeader",
        setup() {
            const store = Store;
            const auth = computed(() => store.state.authenticated)
            const logout = async () => {
                await fetch('http://localhost:3000/api/contacts/logout', {
                    method: 'POST',
                    headers: {"Content-Type": "application/json"},
                    credentials: 'include'
                })
                await store.dispatch('setAuth', false); //Add this line to redirect to login route
            }
            return {
                auth,
                logout
            }
        }
        
    }
</script>

<style>
.nav-item {
    display: flex;
    align-items: center;
}
</style>