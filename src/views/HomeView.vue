<template>
  <div class="home">
   
    <h1>signUp</h1>
    <p><input type="text" placeholder="email" v-model="email"/></p>
    <p><input type="password" placeholder="Password" v-model="password"/></p>
    <button @click="signUp">Sign up</button>
    <p>{{ crederror }}</p>
    
    <button @click="login">Login</button>
  </div>
  
</template>

<script>
// @ is an alias to /src
import { ref } from "vue";
import { getAuth, createUserWithEmailAndPassword ,signInWithEmailAndPassword} from "firebase/auth";
// Import the functions you need from the SDKs you need
import { initializeApp } from "firebase/app";
// TODO: Add SDKs for Firebase products that you want to use
// https://firebase.google.com/docs/web/setup#available-libraries

// Your web app's Firebase configuration
const firebaseConfig = {
  apiKey: "AIzaSyCIjWYLSIkSghQ1T6zGnVyJ_8U-H9xVI0M",
  authDomain: "testing2-eb9c5.firebaseapp.com",
  projectId: "testing2-eb9c5",
  storageBucket: "testing2-eb9c5.appspot.com",
  messagingSenderId: "329757961053",
  appId: "1:329757961053:web:c220873eb798bb3c3696b4"
};

// Initialize Firebase
const firebase = initializeApp(firebaseConfig);

export default {
  name: 'HomeView',
  data() {
    return {
      email: ref(""),
      password: ref(""),
      crederror: ref("")
    };
  },
  methods: {
    async signUp() {
      try {
        const auth = getAuth(firebase);
        const userCredential = await createUserWithEmailAndPassword(auth, this.email, this.password);
        const user = userCredential.user;
        console.log("Successful registration");
        console.log("New user:", user);
        this.$router.push('/about') 
      }  catch (error) {
        console.error("error->",error.message); 
        this.crederror=error.message;
        // Capture the error parameter here
      }
    },
    async login() {
      console.log("midway");
      try {
        const auth = getAuth(firebase); // Corrected the variable name
        const userCredential = await signInWithEmailAndPassword(auth, this.email, this.password);
        const user = userCredential.user;
        console.log("Successful logged in");
        console.log("Logged in user:", user);
        this.$router.push('/about');
      } catch (error) {
        console.error("error->",error.message);
        this.crederror=error.message;
      }
    }
  },
 
  
  };
</script>





