import { createUserWithEmailAndPassword } from "https://www.gstatic.com/firebasejs/10.7.0/firebase-auth.js";

// SIGNUP FUNCTION
window.signup = function(event) {
    event.preventDefault();

    let email = document.getElementById("email").value;
    let password = document.getElementById("password").value;

    createUserWithEmailAndPassword(auth, email, password)
    .then(() => {
        alert("Account created!");
        window.location.href = "login.html";
    })
    .catch((error) => {
        alert(error.message);
    });
}