<template>
  <div id="main">
    <div class="calc">
      <div class="heading">
        <h1>Marks Calculator</h1>
      </div>

      <form @submit.prevent="calculateResult">
        <div class="form-floating mb-3">
          <input
            type="text"
            class="form-control"
            placeholder="name"
            v-model="name"
            required
          />
          <label for="name">Student Name</label>
        </div>
        <div class="input-fields">
          <div class="form-floating mb-3 group">
            <input
              type="number"
              class="form-control"
              placeholder="hindi"
              v-model="marks.hindi"
              required
            />
            <label for="hindi">Hindi</label>
          </div>
          <div class="form-floating mb-3 group">
            <input
              type="number"
              class="form-control"
              placeholder="science"
              v-model="marks.science"
              required
            />
            <label for="science">Science</label>
          </div>
          <div class="form-floating mb-3 group">
            <input
              type="number"
              class="form-control"
              placeholder="english"
              v-model="marks.english"
              required
            />
            <label for="english">English</label>
          </div>
          <div class="form-floating mb-3 group">
            <input
              type="number"
              class="form-control"
              placeholder="maths"
              v-model="marks.maths"
              required
            />
            <label for="maths">Maths</label>
          </div>
          <div class="form-floating mb-3 group">
            <input
              type="number"
              class="form-control"
              placeholder="computer"
              v-model="marks.computer"
              required
            />
            <label for="computer">Computer</label>
          </div>
        </div>
        <div class="bt p-3">
          <button class="button" type="submit">Calculate Result</button>
        </div>
      </form>
    </div>
    <div class="show">
      <h3 v-if="result == null">Result:</h3>
      <div class="result" v-if="result !== null">
        <h3>Result:</h3>
        <h3 class="p-3">Name: {{ this.name }}</h3>
        <ul>
          <li>
            <p>Total Marks: {{ totalMarks }}</p>
          </li>
          <li>
            <p v-if="percentage !== null && percentage !== undefined">
              Percentage: {{ percentage.toFixed(2) }}%
            </p>
          </li>
          <li>
            <p>Grade: {{ grade }}</p>
          </li>
          <li>
            <p v-if="pass">Congratulations! You have passed.</p>
            <p v-else style="color: red">Sorry! You have failed.</p>
          </li>
        </ul>
      </div>
    </div>
    <div class="grade-system">
      <h3>Grade System:</h3>
      <br />
      <p>Result > 90 : "you did great | A"</p>
      <p>Result > 75: "keep working | B"</p>
      <p>Result > 60: "can do better | C"</p>
      <p>Result > 45: "need hard work | D"</p>
      <p>Result > 33: "Quit studying | F"</p>
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
      } else if (percentage >= 33) {
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
  padding: 20px;
  margin: 60px 190px 250px;
  background-color: #141414;
  border-radius: 25px;
  overflow: hidden;
}

.heading {
  text-align: center;
  color: white;
  font: 2.5em poppins;
  margin: 40px 20px 40px;
}
.calc {
  border: 1px solid #333;
  border-radius: 15px;
  padding: 20px;
  background-color: #1f1f1f;
}

.input-fields {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: space-around;
}

input[type="text"],
input[type="number"] {
  background: #292929;
  border: none;
  border-radius: 15px;
  color: white;
}

label {
  color: white;
}
.group {
  flex: 1;
  margin-right: 10px;
  width: calc(20% - 10px); /* Adjust width to 20% and subtract margin */
}

.bt {
  text-align: center;
}

.button {
  padding: 15px 25px;
  margin: 20px;
  background-size: 200% auto;
  color: white;
  border-radius: 15px;
  background: #4a8400;
}
button:hover {
  background-color: #0056b3;
}
.result ul {
  display: flex;
  justify-content: space-around;
  flex-wrap: wrap;
  list-style: none;
  background: #292929;
  border-radius: 15px;
  padding: 30px 20px;
  margin: 20px;
}

.result h2 {
  margin-bottom: 10px;
}

.show {
  margin: 20px 0;
  padding: 20px;
  width: 100%;
  color: white;
  background-color: #1f1f1f;
  border-radius: 15px;
  border: 1px solid #333;
}
.grade-system {
  color: #757575;
}
</style>
