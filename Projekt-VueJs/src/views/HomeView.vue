<template>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.3.0/font/bootstrap-icons.css" />
  <div class="home">
    <div class="grid-top-container">
      <div class="grid-item">
        <h1>Notenverwaltungstool</h1>
      </div>
      <div class="grid-item">
        <button class="btn btn-Dark" v-on:click="openForm()">
          <h1 class="bi bi-plus-circle-fill"></h1>
        </button>
      </div>
    </div>
    <div class="form-popup" id="myForm">
      <div class="form-container">
        <h1>Neues Fach</h1>

        <label for="text"><b>Fachname</b></label>
        <input type="text" placeholder="Fachname" name="fachName" v-model="newSubject">

        <button type="submit" class="btn" v-on:click="addSubject($event)">Speichern</button>
        <button type="button" class="btn cancel" v-on:click="closeForm()">Abbrechen</button>
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
            <h3>Durchschnitt: {{ grades.avg }}</h3>
          </div>
          <div>
            <input v-on:keyup.enter="addGrade($event, subject)" placeholder="Gib eine neue Note ein" /><br />
          </div>
        </div>
      </div>
      <h2>Gesammt Durchschnitt: {{ computedAverage }}</h2>
    </div>
  </div>
</template>

<script>
import { computed } from '@vue/reactivity';
import { ref } from 'vue'

export default {
  name: 'HomeView',
  setup: () => {
    const newSubject = ref("");

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
    }

    const computedAverage = computed(() => {
      let averageTemp = 0
      let amountOfGrades = 0
      for (let subject in subjects.value) {
        for (let grade of subjects.value[subject].subjectArray) {
          averageTemp += parseFloat(grade)
          amountOfGrades++
        }
      }
      return  Math.round((averageTemp / amountOfGrades)*2) / 2
    })

    function addSubject(e) {
      subjects.value[newSubject.value] = {
        subjectArray: [],
        avg: 0
      }
      newSubject.value = "";
    }

    function addGrade(e, subject) {
      let tempGrade = e.target.value
      tempGrade = parseFloat(tempGrade).toFixed(2)
      if (isNaN(tempGrade))
        alert("Das ist keine Nummer.")
      else if (tempGrade > 6)
        alert("Die nummer muss zwischen 1 und 6 liegen.")
      else if (tempGrade < 1)
        alert("Die nummer muss zwischen 1 und 6 liegen.")
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

    function openForm() {
      document.getElementById("myForm").style.display = "block";
    }

    function closeForm() {
      document.getElementById("myForm").style.display = "none";
    }

    return {
      subjects,
      addGrade,
      deleteGrade,
      openForm,
      closeForm,
      addSubject,
      newSubject,
      computedAverage
    }
  }
}
</script>
