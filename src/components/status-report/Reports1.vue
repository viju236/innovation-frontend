 <template>
   <div class="reports">
     <div class="row">
       <div class="flex xs12">
         <div class="row">
           <div class="flex md4 sm6 xs12">
             <input type="text" class="input-control" id="devTeam" list="devTeams" v-model="devTeam"
               placeholder="DEV TEAM" />
             <datalist id="devTeams">
               <option v-for="(value, key) in devTeams" :key="key">
                 {{ value.description }}
               </option>
             </datalist>
           </div>

           <div class="flex md4 sm6 xs12">
             <input type="text" class="input-control" id="ScrumTeam" list="scrumTeams" v-model="SelectedscrumTeams"
               placeholder="SCRUM TEAM" />
             <datalist id="scrumTeams">
               <option v-for="(value, key) in scrumTeams" :key="key">
                 {{ value.name }}
               </option>
             </datalist>
           </div>

           <div class="flex md4 sm6 xs12">
             <input type="text" class="input-control" id="team" list="Options" v-model="SelectedTeam"
               placeholder="DESKTOP/CLOUD" />
             <datalist id="Options">
               <option v-for="(value, key) in Options" :key="key">
                 {{ value.name }}
               </option>
             </datalist>
           </div>

           <div class="flex md4 sm6 xs12">
             <input type="text" class="input-control" id="location" list="Locations" v-model="SelectedLocations"
               placeholder="Location" />
             <datalist id="Locations">
               <option v-for="(value, key) in Locations" :key="key">
                 {{ value.name }}
               </option>
             </datalist>
           </div>

           <div class="flex md4 sm6 xs12">
             <input type="text" class="input-control" id="manager" list="managerName" v-model="SelectedManager"
               placeholder="Manager" />
             <datalist id="managerName">
               <option v-for="(value, key) in managerName" :key="key">
                 {{ value.name }}
               </option>
             </datalist>
           </div>

           <div class="flex md4 sm6 xs12">
             <button class="button" @click="submitData">Submit</button>
           </div>
         </div>
       </div>
     </div>
   </div>
   <div class="card">
     <div class="cards-container row d-flex wrap align--start">
       <div class="flex xs12">
         <label><b>STATUS REPORT</b></label>
       </div>
     </div>
   </div>
 </template>
 <script>
   export default {
     name: 'reports1',
     data() {
       return {
         SelecteddevTeams: [],
         SelectedscrumTeams: [],
         SelectedTeam: [],
         SelectedLocations: [],
         SelectedManager: [],
         selected: 'A',
         devTeams: [{
             id: 1,
             description: 'Team 1',
           },
           {
             id: 2,
             description: 'Team 2',
           },
           {
             id: 3,
             description: 'Team 3',
           }
         ],
         scrumTeams: [{
             id: 1,
             name: 'Simple Minds'
           },
           {
             id: 2,
             name: 'Avengers'
           },
           {
             id: 3,
             name: 'KFP'
           }
         ],
         Options: [{
             id: 1,
             name: "Cloud"
           },
           {
             id: 2,
             name: "Desktop"
           }
         ],
         Locations: [{
             id: 1,
             name: "Pune"
           },
           {
             id: 2,
             name: "HST"
           }
         ],
         managerName: [{
             id: 1,
             name: "Ninad Kulkarni"
           },
           {
             id: 2,
             name: "Rahul Kulkarni"
           }
         ],

       }

     },
     methods:{
         submitData(){
             console.log('in function----',devTeam);
             console.log('SelectedscrumTeams---',this.SelectedscrumTeams);
            //   console.log('SelectedTeam---',SelectedTeam);
            //    console.log('SelectedLocations---',SelectedLocations);
            //     console.log('SelectedManager---',SelectedManager);
         }
     }
   }
 </script>

 <style lang="scss">
   .input-control {
     padding: 4px;
     margin: 10px 25px;
     border-radius: 4px;
     width: 400px;
   }

   .label-control {
     width: 200px;
   }

   .container {
     margin-top: 50px;
     display: grid;
     width: 100%;
     grid-template-columns: 135px auto auto;
     // grid-template-columns: repeat(3, auto);
     align-items: center;
   }

   .imagePreview {
     width: 100px;
     height: 100px;
     margin-right: 20px;
   }

   .editor-control {
     margin-top: 30px;
     height: 300px;
   }

   .image-control {
     position: relative;
     top: 10px;
     right: 2px;
   }

   .row {
     
     background-image: url("cover1.jpg");
     background-repeat: no-repeat;
     background-size: cover;
   }

   .button {
     background-color: blue;
     border: none;
     color: white;
     padding: 15px 32px;
     text-align: center;
     text-decoration: none;
     display: inline-block;
     font-size: 16px;
     margin: 4px 2px;
     cursor: pointer;
     border-radius: 28px;
   }

   .container1 {
     margin-top: 50px;
     
     width: 100%;
    
     align-items: center;
   }

   .card {
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
  max-width: 100%;
  margin: auto;
  text-align: center;
  font-family: arial;
  margin-top: 50px;
  background-image: url("cover.jpg");
  background-repeat: no-repeat;
  background-size: cover;
  height: 481px;
}

 </style>
