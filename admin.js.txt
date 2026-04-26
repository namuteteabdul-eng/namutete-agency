import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.0/firebase-app.js";
import { getAuth, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/10.7.0/firebase-auth.js";
import { getFirestore, collection, getDocs } from "https://www.gstatic.com/firebasejs/10.7.0/firebase-firestore.js";

// 🔴 PUT YOUR FIREBASE CONFIG HERE
const firebaseConfig = {
  apiKey: "YOUR_KEY",
  authDomain: "YOUR_DOMAIN",
  projectId: "YOUR_ID"
};

const app = initializeApp(firebaseConfig);
const auth = getAuth(app);
const db = getFirestore(app);

// 🔴 CHANGE THIS TO YOUR EMAIL
const ADMIN_EMAIL = "yourname@gmail.com";

// 🔐 PROTECT ADMIN PAGE
onAuthStateChanged(auth, (user) => {
    if (!user) {
        window.location.href = "login.html";
    } else if (user.email !== ADMIN_EMAIL) {
        window.location.href = "dashboard.html";
    } else {
        loadMessages();
    }
});

// 📩 LOAD MESSAGES
async function loadMessages() {
    const messageList = document.getElementById("messageList");

    const querySnapshot = await getDocs(collection(db, "messages"));

    querySnapshot.forEach((doc) => {
        let data = doc.data();
        let li = document.createElement("li");
        li.textContent = data.name + " | " + data.email + " | " + data.message;
        messageList.appendChild(li);
    });
}