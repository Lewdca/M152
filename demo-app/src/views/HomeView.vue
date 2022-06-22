<template>
  <div class="home">
    <h1>Notenverwaltungstool</h1>

    <div class="grid-container">
      <div v-for="(grades, subject) in subjects" class="grid-item">
        {{ subject }} <br />
        <div v-for="grade in grades.subjectArray">
          {{ grade }}
          <input type="button" v-on:click="deleteGrade(grade, subject)" value="Löschen"/>
        </div>
        <div>
          Avarage: {{ grades.avg }}
        </div>
        <input v-on:keyup.enter="addGrade($event, subject)" placeholder="Gib eine neue Note ein" /><br />
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue'

export default {
  name: 'HomeView',
  setup: () => {
    let subjectAvg

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

    function avgFunction(){
      subjects.forEach(element =>{
  
      })
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

    function deleteGrade(grade, subject){
     let arrayLength = subjects.value[subject].subjectArray.length;
     for(var i = 0; i < arrayLength; i++){
       if(subjects.value[subject].subjectArray[i] === grade){
         subjects.value[subject].subjectArray.splice(i, 1);
       }
     }
    }

    return {
      subjects,
      addGrade,
      deleteGrade
    }
  }
}
</script>
