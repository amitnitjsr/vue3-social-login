<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h2 v-if="user">Signed In User: {{ user }}</h2>

    <br>
    <div id="logout" v-if="isSignedIn">
      <button @click="handleSignOut">logout</button>
    </div>

    <br>
    <div id="GoogleSignIn" v-if="!isSignedIn">
      <h3>Google Signin</h3>
      <button @click="handleSignInGoogle">Login</button>
    </div>

    <br>
    <div id="TwitterSignIn" v-if="!isSignedIn">
      <h3>Twitter Signin</h3>
      <button @click="handleSignInTwitter">Login</button>
    </div>

    <br>
    <div id="GitHubSignIn" v-if="!isSignedIn">
      <h3>GitHub Signin</h3>
      <button @click="handleSignInGitHub">Login</button>
    </div>
  </div>
</template>

<script>
import firebaseConfig from '../firebaseConfig';
import { getAuth, signInWithPopup, signOut, GoogleAuthProvider, TwitterAuthProvider, GithubAuthProvider } from "firebase/auth";

firebaseConfig

const provider = new GoogleAuthProvider();
const providerTwitter = new TwitterAuthProvider();
const providerGithub = new GithubAuthProvider();
const auth = getAuth();

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      user: '',
      isSignedIn: false,
    }
  },
  methods: {

    handleSignInGoogle() {
      signInWithPopup(auth, provider)
        .then((result) => {          
          this.user = result.user.displayName;
          this.isSignedIn = true;
        }).catch((error) => {
          console.log(error);
        });
    },

    handleSignInTwitter() {
      signInWithPopup(auth, providerTwitter)
        .then((result) => {          
          this.user = result.user.displayName;
          this.isSignedIn = true;
        }).catch((error) => {
          console.log(error);
        });
    },

    handleSignInGitHub() {
      signInWithPopup(auth, providerGithub)
        .then((result) => {          
          this.user = result.user.displayName;
          this.isSignedIn = true;
        }).catch((error) => {
          console.log(error);
        });
    },
    
    handleSignOut() {
      signOut(auth).then(() => {
          this.user = '';
          this.isSignedIn = false;
        }).catch((error) => {
          console.log(error);
        });
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
button {
    color: #42b983;
    background-color: azure;
    height: 30px;
    width: 100px;
    border-radius: 8px;
    border-style: solid;
    border-color: cadetblue;
}
</style>
