<template>
  <div class="app">
    <!-- Loader / Intro -->
    <div v-if="step === 'loader'" class="loader">
      <img src="https://cdn-icons-png.flaticon.com/512/616/616408.png" alt="Bouquet" class="bouquet" />
      <h2>Madame Laetitia Casal</h2>
    </div>

    <!-- Page date -->
    <div v-else-if="step === 'date'" class="date-step">
      <p>Pour accéder à la question, entre notre date de couple :</p>
      <input v-model="enteredDate" type="date" />
      <button @click="checkDate">Valider</button>
      <p v-if="error" class="error">{{ error }}</p>
    </div>

    <!-- Question finale -->
    <div v-else-if="step === 'question'" class="question-step">
      <p>Accepte-tu d'être ma petite copine pour la vie ?</p>
      <button @click="answerYes" class="yes">Oui ❤️</button>
      <button @click="answerNo" class="no">Non 😢</button>
      <p v-if="message" class="message">{{ message }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      step: "loader",          // 'loader' → 'date' → 'question'
      enteredDate: "",
      correctDate: "2024-01-06",
      error: "",
      message: "",
      noCount: 0,
    };
  },
  mounted() {
    // Affiche le loader 2s puis passe à la date
    setTimeout(() => {
      this.step = "date";
    }, 2000);
  },
  methods: {
    checkDate() {
      if (this.enteredDate === this.correctDate) {
        this.step = "question";
        this.error = "";
      } else {
        this.error = "Hmm, ce n'est pas la bonne date 😅";
      }
    },
    answerYes() {
      this.message = "Bon toutou 🐶";
    },
    answerNo() {
      this.noCount++;
      if (this.noCount >= 3) {
        this.message = "Appuie sur Oui pour éviter le bug 😜";
      } else {
        this.message = "Veuillez réessayer 😢";
      }
    }
  }
};
</script>

<style scoped>
.app {
  max-width: 500px;
  margin: 100px auto;
  text-align: center;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  background-color: #fffaf0;
  padding: 30px;
  border-radius: 12px;
  box-shadow: 0 0 20px rgba(0,0,0,0.15);
}

/* Loader */
.loader {
  display: flex;
  flex-direction: column;
  align-items: center;
  animation: fadeIn 1.5s ease-in-out;
}

.bouquet {
  width: 100px;
  height: 100px;
  animation: bounce 2s infinite;
}

@keyframes bounce {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-15px); }
}

/* Input date */
.date-step input[type="date"] {
  padding: 8px;
  font-size: 16px;
  margin-right: 10px;
  border-radius: 5px;
  border: 1px solid #ccc;
}

button {
  padding: 10px 20px;
  font-size: 16px;
  cursor: pointer;
  border-radius: 5px;
  border: none;
  transition: transform 0.1s;
}

button:hover {
  transform: scale(1.05);
}

button.yes {
  background-color: #4caf50;
  color: white;
}

button.no {
  background-color: #f44336;
  color: white;
}

.error {
  color: red;
  margin-top: 10px;
}

.message {
  margin-top: 20px;
  font-size: 20px;
  font-weight: bold;
  color: #333;
}

/* Animations */
@keyframes fadeIn {
  from { opacity: 0; }
  to { opacity: 1; }
}
</style>
