<template>
  <div>
      <div class = 'bg-blue-900 border-4 border-red-700 text-4xl text-white  w-full font-bold text-left p-2'><b>GPA Calculator</b>:  Edison GPA System</div>
      <div class = 'float-left inline-block bg-blue-300  border-4 border-black m-2 w-1/2 h-96 overflow-y-auto'> 
         <div v-for = "(item, index) of data" :key = "item.id"> 
              <span> 
                  <input
                     type = 'text'
                     :placeholder = "'Course ' + (index + 1)"
                     class = 'p-2 m-2 border-2 border-black'
                     v-model = "item.course"
                     
                  >
                  <input
                    type = 'text'
                    placeholder = "Credit Value"
                    class = 'p-2 m-2 border-2 border-black'
                    v-model = "item.credits"
                  >
                  <select v-model = 'item.type' class = 'p-1 m-1 border-2 border-black' id="type">
                    <option value="ap">AP/Honors</option>
                    <option value="1">Level 1</option>
                    <option value="2">Level 2</option>
                  </select>
                   <select  class = 'p-1 m-1 border-2 border-black' id="cars" value = "Grades" v-model = 'item.points'>
                       <option value="4.33">A+</option>
                       <option value="4.00">A </option>
                       <option value="3.67">A-</option>
                       <option value="3.33">B+</option>
                       <option value="3.00">B </option>
                       <option value="2.67">B-</option>
                       <option value="2.33">C+</option>
                       <option value="1.00">C </option>
                       <option value="1.67">C-</option>
                       <option value="1.00">D </option>
                       <option value="0.00">F </option>
                  </select>
              </span>
         </div>
      </div>
      <div> 
          <div class = 'my-9 text-4xl'> 
               <b>Unweighted GPA</b><br> <h1 :class = 'color' class = 'font-bold text-6xl'>{{ (this.unweighted).toFixed(2) }}</h1>
               <br>
               <b>Weighted GPA </b> <br> <h1 class = 'text-blue-900 font-bold text-6xl'> {{ (this.weighted).toFixed(2) }} </h1>
               <br> 
               <b>Status</b> <br><h1> <h1 :class = 'color' class = 'font-bold text-6xl'> {{ this.status }}  </h1></h1>
          </div>
      </div>
         <div class = 'bg-indigo-900 border-4 border-white m-2 w-1/2'> 
              <button @click = 'calculate()' class = 'rounded p-2 m-2 bg-yellow-600 text-white'><b>Calculate</b></button>
              <button @click = 'addCourse()' class = 'rounded p-2 m-2 bg-green-600 text-white'><b>Add Course</b></button>
              <button @click = 'removeCourse()' class = 'rounded p-2 m-2 bg-red-500 text-white'><b>Remove Course</b></button>
          </div>
      <br> 
      <div> 
         Instructions: Input the requested information into the calculator, so that you can calculate the GPA. Note that this is in the Edison School District GPA System, so it is on the 4.33 scale. It is a useful tool to track GPA on Edison Standards throughout the school year, so you know where to work on!
      </div>
    </div>
</template>

<script>
export default {
     data() { 
        return { 
            data: [
               { 
                  course: "", 
                  id: Math.random(),
                  credits: "",
                  type: "", 
                  points: ""
               },
               { 
                  course: "", 
                  id: Math.random(),
                  credits: "",
                  type: "", 
                  points: ""
               },
               { 
                  course: "", 
                  id: Math.random(),
                  credits: "",
                  type: "", 
                  points: ""
               },
               { 
                  course: "", 
                  id: Math.random(),
                  credits: "",
                  type: "", 
                  points: ""
               }
               ,{ 
                  course: "", 
                  id: Math.random(),
                  credits: "",
                  type: "", 
                  points: ""
               },
               { 
                  course: "", 
                  id: Math.random(),
                  credits: "",
                  type: "", 
                  points: ""
               },
               { 
                  course: "", 
                  id: Math.random(),
                  credits: "",
                  type: "", 
                  points: ""
               },
            ], 
            unweighted: 0,
            color: "text-black",
            weighted: 0, 
            status: "...",
        }
     }, 
     methods: { 
          calculate() { 
         // Unweighted
            let totalPoints = 0; 
            let credits = 0; 
                   for (let course of this.data) { 
                         totalPoints = totalPoints + (parseFloat(course.credits) * parseFloat(course.points)); 
                         credits += parseFloat(course.credits); 
                   }
              this.unweighted = (totalPoints/credits); 
        // Weighted  
          let weightedPoints = 0; 
                 for (let course of this.data) { 
                        if (course.type == "ap") { 
                             weightedPoints += (parseFloat(course.credits) * (parseFloat(course.points) + 2.00));
                        }
                        else if (course.type == '1') { 
                            weightedPoints += (parseInt(course.credits) * (parseFloat(course.points) + 1.00));
                        }
                        else { 
                            weightedPoints += (parseFloat(course.credits) * (parseFloat(course.points)));
                        }
                  }
              this.weighted = (weightedPoints /credits); 
              if (this.unweighted > 4.00) { 
                  this.status = "Excellent 😊";
                  this.color = 'text-green-600'
              }
              else if (this.unweighted >= 3.65) { 
                  this.status = "Good 🙂";
                  this.color = 'text-green-400'
              }
              else if (this.unweighted >= 3.00) { 
                  this.status = "OK 😐";
                  this.color = 'text-yellow-600'
              }
              else if (this.unweighted >= 2.00) { 
                  this.status = "Poor";
                  this.color = 'text-yellow-600'
              }
              else if (this.unweighted <= 2.50) { 
                  this.status = "Failing";
                  this.color = 'text-red-500'
              }
          
          }, 
          addCourse() { 
                this.data.push({ 
                    course: "", 
                    id: Math.random(), 
                    credits: 0, 
                    type: "", 
                    points: "",
                })
          }, 
          removeCourse() { 
              this.data.pop();  
          }
     }
}
</script>

<style>
</style>