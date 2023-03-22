<template>
    <nav>
        <h1>Gatcha Game</h1>       
      
    </nav>
    <div v-if="isLogin" class="login">
    <button @click="signOut" > Sign Out</button>
    </div>
    <div v-else >
        <button @click="signIn">Sign In</button>
    
    </div>
    </template>
    <script>
       import { useAuth, currentUser} from '@/firebase'


       export default {
        setup() {
            const { user, isLogin, signOut, signIn, currentUser } = useAuth()
            
            return  { user, isLogin, signOut, signIn, currentUser }
        },               
       }
      
    </script>

    <style scoped>
        *{
            text-align:center;
            margin: 10px;
        }
    </style>