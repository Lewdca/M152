<template>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.3.0/font/bootstrap-icons.css" />
  <div class="home">
    <div class="grid-top-container">
      <div class="grid-item">
        <h1>Notenverwaltungstool</h1>
      </div>
      <div class="grid-item">
        <button class="btn btn-Dark">
          <h1 class="bi bi-plus-circle-fill"></h1>
        </button>
      </div>
    </div>
    <div class="grid-container">
      <div v-for="(grades, subject) in subjects" class="grid-item">
        <h2>{{ subject }} </h2><br />
        <div class="flex-container">
          <div v-for="grade in grades.subjectArray">
            <h3>
              {{ grade }}
              <button class="btn btn-danger" v-on:click="deleteGrade(grade, subject)">
                <i class="bi bi-trash-fill"></i>
              </button>
            </h3>
          </div>
          <div>
            <h3>Avarage: {{ grades.avg }}</h3>
          </div>
          <div>
            <input v-on:keyup.enter="addGrade($event, subject)" placeholder="Gib eine neue Note ein" /><br />
          </div>
        </div>
      </div>
      <h2>Durchschnitt: {{ average }}</h2>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue'

export default {
  name: 'HomeView',
  setup: () => {
    let subjectAvg
    let average

    let subjects = ref({
      "GES": {
        subjectArray: [],
        avg: 0
      },
      "SPK": {
        subjectArray: [],
        avg: 0
      },
      "WUR": {
        subjectArray: [],
        avg: 0
      },
      "NWS": {
        subjectArray: [],
        avg: 0
      },
      "INF151": {
        subjectArray: [],
        avg: 0
      },
      "INF152": {
        subjectArray: [],
        avg: 0
      },
      "INF153": {
        subjectArray: [],
        avg: 0
      },
      "INF306": {
        subjectArray: [],
        avg: 0
      }
    })

    function subjectAvgFunciton(subject) {
      let temp = 0
      let subjectAvg = 0
      subjects.value[subject].subjectArray.forEach(element => {
        temp += parseFloat(element)
      })
      subjectAvg = temp / subjects.value[subject].subjectArray.length
      subjects.value[subject].avg = subjectAvg.toFixed(2)
      avgFunction()
    }

    function avgFunction() {
      let averageTemp = 0
      let amountOfGrades = subjects.length
      subjects.forEach(element => {
        averageTemp += element.avg
      })
      average = averageTemp / amountOfGrades
    }

    function addGrade(e, subject) {
      let tempGrade = e.target.value
      if (tempGrade > 6)
        console.log("Can't be higher than 6")
      else if (tempGrade < 1)
        console.log("Can't be lower than 1")
      else {
        subjects.value[subject].subjectArray.push(tempGrade)
        subjectAvgFunciton(subject)
      }
    }

    function deleteGrade(grade, subject) {
      let arrayLength = subjects.value[subject].subjectArray.length;
      for (var i = 0; i < arrayLength; i++) {
        if (subjects.value[subject].subjectArray[i] === grade) {
          subjects.value[subject].subjectArray.splice(i, 1);
          break;
        }
      }
    }

    return {
      subjects,
      average,
      addGrade,
      deleteGrade,
    }
  }
}
</script>
