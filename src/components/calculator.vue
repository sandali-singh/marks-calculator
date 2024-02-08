<template>
  <div id="main">
    <div class="heading">
      <h1>Marks Calculator</h1>
    </div>
    <div class="calc">
      <div class="input-fields">
        <form @submit.prevent="calculateResult">
          <div class="input-field">
            <label for="name">Student Name:</label>
            <input type="text" id="name" v-model="name" required />
          </div>
          <div class="input-field">
            <label for="maths">Maths:</label>
            <input type="number" id="maths" v-model="marks.maths" required />
          </div>
          <div class="input-field">
            <label for="science">Science:</label>
            <input
              type="number"
              id="science"
              v-model="marks.science"
              required
            />
          </div>
          <div class="input-field">
            <label for="english">English:</label>
            <input
              type="number"
              id="english"
              v-model="marks.english"
              required
            />
          </div>
          <div class="input-field">
            <label for="hindi">Hindi:</label>
            <input type="number" id="hindi" v-model="marks.hindi" required />
          </div>
          <div class="input-field">
            <label for="computer">Computer:</label>
            <input
              type="number"
              id="computer"
              v-model="marks.computer"
              required
            />
          </div>
          <button type="submit">Calculate Result</button>
        </form>
      </div>
      <div class="show">
        <div class="result" v-if="result !== null">
          <h2>Result:</h2>
          <h3>{{ this.name }}</h3>
          <p>Total Marks: {{ totalMarks }}</p>
          <p>CGPA: {{ averageMarks }}</p>
          <p v-if="percentage !== null && percentage !== undefined">
            Percentage: {{ percentage.toFixed(2) }}%
          </p>
          <p>Grade: {{ grade }}</p>
          <p v-if="pass">Congratulations! You have passed.</p>
          <p v-else style="color: red">Sorry! You have failed.</p>
        </div>
        <div class="grade-system">
          <p>Result > 90 : "you did great | A"</p>
          <p>Result > 75: "keep working | B"</p>
          <p>Result > 60: "can do better | C"</p>
          <p>Result > 45: "need hard work | D"</p>
          <p>Result > 33: "Quit studying | F"</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "marks-calculator",
  data() {
    return {
      name: "",
      marks: {
        maths: null,
        science: null,
        english: null,
        hindi: null,
        computer: null,
      },
      result: null,
    };
  },
  computed: {
    totalMarks() {
      return (
        parseInt(this.marks.maths || 0) +
        parseInt(this.marks.science || 0) +
        parseInt(this.marks.english || 0) +
        parseInt(this.marks.hindi || 0) +
        parseInt(this.marks.computer || 0)
      );
    },
    averageMarks() {
      return this.totalMarks / 5;
    },
    pass() {
      return this.averageMarks >= 40;
    },
    percentage() {
      const totalMarks = this.totalMarks;
      const maxMarks = 500; // Assuming max marks for each subject is 100
      return (totalMarks / maxMarks) * 100;
    },
    grade() {
      const percentage = this.percentage;
      if (percentage >= 90) {
        return "you did great";
      } else if (percentage >= 75) {
        return "keep working";
      } else if (percentage >= 60) {
        return "can do better";
      } else if (percentage >= 45) {
        return "need hard work";
      } else {
        return "Quit studying";
      }
    },
  },
  methods: {
    calculateResult() {
      this.result = true;
    },
  },
};
</script>

<style>
#main {
  padding: 0 140px;
}

.heading {
  text-align: center;
  color: #333;
  font: 2.5em sans-serif;
}
.calc {
  border: 1px solid #eee;
  border-radius: 15px;
  padding: 20px;
  margin-top: 20px;
  background-color: #92c7cf;
  max-width: 1200px;
  box-sizing: border-box;
}

.input-fields {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-gap: 10px;
}

.input-field {
  display: flex;
  flex-direction: column;
}

label {
  margin-bottom: 5px;
  color: #555;
}

input[type="number"] input[type="text"] {
  padding: 8px;
  border: 1px solid #ccc;
}

button {
  display: block;
  width: 100%;
  padding: 10px;
  margin-top: 10px;
  background-color: #007bff;
  color: #fff;
  border: none;
  border-radius: 8px;
  cursor: pointer;
}

button:hover {
  background-color: #0056b3;
}

.result {
  display: flex;
  justify-content: space-evenly;
  flex-wrap: wrap;
}

.result h2 {
  margin-bottom: 10px;
}
.show {
  margin-top: 20px;
  border-top: 1px solid #ccc;
  padding-top: 10px;
  width: 100%;
  color: #555;
}
</style>
