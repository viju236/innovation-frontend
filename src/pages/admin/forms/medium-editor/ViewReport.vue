<template>
  <div class="reports">
    <div class="row">
      <div class="flex xs12">
        <div class="row">
          <div class="filter-control">
            <input
              type="text"
              class="input-control"
              id="devTeam"
              list="devTeams"
              v-model="devTeam"
              placeholder="Dev Team"
            />
            <datalist id="devTeams">
              <option v-for="team in devTeams" :key="team">
                 {{ team }}
               </option>
            </datalist>

            <input
              type="text"
              class="input-control"
              id="ScrumTeam"
              list="scrumTeams"
              v-model="SelectedscrumTeams"
              placeholder="Scrum Team"
            />
            <datalist id="scrumTeams">
              <option v-for="team in scrumTeams" :key="team">
                 {{ team }}
               </option>
            </datalist>

            <input
              type="text"
              class="input-control"
              id="team"
              list="Options"
              v-model="SelectedTeam"
              placeholder="Desktop/Cloud"
            />
            <datalist id="Options">
              <option v-for="(value, key) in Options" :key="key">
                {{ value.name }}
              </option>
            </datalist>

            <input
              type="text"
              class="input-control"
              id="location"
              list="Locations"
              v-model="SelectedLocations"
              placeholder="Location"
            />
            <datalist id="Locations">
              <option v-for="(value, key) in Locations" :key="key">
                {{ value.name }}
              </option>
            </datalist>

            <input
              type="text"
              class="input-control"
              id="manager"
              list="managerName"
              v-model="SelectedManager"
              placeholder="Manager"
            />
            <datalist id="managerName">
              <option v-for="manager in managerName" :key="manager">
                 {{ manager }}
               </option>
            </datalist>

          </div>
          <div class="submit-control">
            <button class="button" @click="submitData">Submit</button>
          </div>
        </div>
      </div>
    </div>
  </div>
  <div class="card">
    <div class="cards-container row d-flex wrap align--start">
      <div class="flex xs12 card-header-control">
        <label><b>STATUS REPORT</b></label>
        
          <div id="reportHtml"></div> <br>
          
    </div>
    </div>
  </div>
</template>
 <script>
 import axios from 'axios';
 import '@vueup/vue-quill/dist/vue-quill.snow.css';
 import { QuillEditor, Quill } from '@vueup/vue-quill'
var quill = new Quill('#editor', {
    theme: 'snow'
});

// var justHtmlContent = document.getElementById('justHtml');

// quill.on('text-change', function() {
// ;
//   var justHtml = "<h1 style='color:red'>Hello Gowtham</h1>";

//   justHtmlContent.innerHTML = justHtml;
// });

export default {
     name: 'ViewReport',
       components: {
        QuillEditor
      },
     data() {
       return {
         SelecteddevTeams: [],
         SelectedscrumTeams: [],
         SelectedTeam: [],
         SelectedLocations: [],
         SelectedManager: [],
         selected: 'A',
         devTeams: [],
         scrumTeams: [],
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
         managerName: [],
         contents : [],
         data: `<p>o&nbsp;&nbsp;<a href="https://mypolarion.industrysoftware.automation.siemens.com/polarion/redirect/project/Mainstream_Engineering_Software/workitem?id=ME-157397" rel="noopener noreferrer" target="_blank">ME-157397</a> - XShare Preprod - Single file download behavior is changed – Fixed (100%)</p><p>o&nbsp;&nbsp;<a href="https://mypolarion.industrysoftware.automation.siemens.com/polarion/redirect/project/Mainstream_Engineering_Software/workitem?id=ME-157421" rel="noopener noreferrer" target="_blank">ME-157421</a> - XShare Preprod US and EU region: In project details page, project cards are not getting displayed – Fixed (100%)</p></div>`
         //data: "&lt;div class="ql-editor" data-gramm="false" contenteditable="true">&lt;p>o&nbsp;&nbsp;&lt;a href="https://mypolarion.industrysoftware.automation.siemens.com/polarion/redirect/project/Mainstream_Engineering_Software/workitem?id=ME-157397" rel="noopener noreferrer" target="_blank">ME-157397&lt;/a> - XShare Preprod - Single file download behavior is changed – Fixed (100%)&lt;/p>&lt;p>o&nbsp;&nbsp;&lt;a href="https://mypolarion.industrysoftware.automation.siemens.com/polarion/redirect/project/Mainstream_Engineering_Software/workitem?id=ME-157421" rel="noopener noreferrer" target="_blank">ME-157421&lt;/a> - XShare Preprod US and EU region: In project details page, project cards are not getting displayed – Fixed (100%)&lt;/p>&lt;/div>&lt;div class="ql-clipboard" contenteditable="true" tabindex="-1">&lt;/div>&lt;div class="ql-tooltip ql-hidden">&lt;a class="ql-preview" rel="noopener noreferrer" target="_blank" href="about:blank">&lt;/a>&lt;input type="text" data-formula="e=mc^2" data-link="https://quilljs.com" data-video="Embed URL">&lt;a class="ql-action">&lt;/a>&lt;a class="ql-remove">&lt;/a>&lt;/div>"

       }

     },
     mounted() {
      axios.get('http://localhost:3000/v1/users/getUniqueFilters').then(response => {
        this.scrumTeams = Object.freeze(response.data.scrumTeam);
        this.devTeams = Object.freeze(response.data.devTeam);
        this.managerName = Object.freeze(response.data.manager);
      })
     },
     methods:{
         submitData(){
             console.log('dev team----',this.SelecteddevTeams.length);
             console.log('scrumTeams---',this.SelectedscrumTeams.length);
             console.log('location---',this.SelectedLocations.length);
             console.log('team---',this.SelectedTeam.length);
             console.log('manager---',this.SelectedManager.length);

             let reportObj = {};

            if(this.SelectedscrumTeams.length > 0) {
              reportObj.scrumTeam = this.SelectedscrumTeams;
            }

            if(this.SelecteddevTeams.length > 0) {
              reportObj.devTeam = this.SelecteddevTeams;
            }

            if(this.SelectedLocations.length > 0) {
              reportObj.location = this.SelectedLocations;
            }

            if(this.SelectedTeam.length > 0) {
              reportObj.teamType = this.SelectedTeam;
            }

            if(this.SelectedManager.length > 0) {
              reportObj.manager = this.SelectedManager;
            }

            axios.post(('http://localhost:3000/v1/users/getReport'), reportObj).then(response => {
              //this.contents = response;
              console.log(response);
              response.data.forEach(res => {
                this.contents.push(res.reports[0].reportContent); 
              })

              let str = decodeURI(`&lt;p>ME-157397 - XShare Preprod - Single file download behavior is changed – Fixed (100%)&lt;/p>&lt;ul>&lt;li>ME-157397 - XShare Preprod - Single file download behavior is changed – Fixed (100%)&lt;/li>&lt;/ul>&lt;ol>&lt;li class="ql-indent-1">ME-157397 - XShare Preprod - Single file download behavior is changed – Fixed (100%)&lt;/li>&lt;/ol>`);

              document.getElementById('reportHtml').innerHTML = str;
            });

            
         },
         span(text) {
          return `<span> ${text} </span>`
        }
     }
   }
</script>

 <style lang="scss">
.input-control {
  padding: 4px;
  margin: 10px 5px;
  border-radius: 4px;
  width: 250px;
  box-shadow: 4px 6px 5px grey;
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
  //   background-image: url("https://source.unsplash.com/user/erondu/1600x600.jpg");
  background-repeat: no-repeat;
  background-size: cover;
}

.button {
  background-color: gray;
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
.card-header-control{
    margin-top: 10px;
}
.filter-control {
  display: grid;
  width: 100%;
  grid-template-columns: repeat(5, auto);
}
.container1 {
  margin-top: 50px;

  width: 100%;

  align-items: center;
}

.submit-control{
    text-align: end;
    width: 100%;
}   

.card {
  box-shadow: 4px 6px 5px grey;
  background-color: white;
  border: 2px solid grey;
  border-radius: 4px;
  max-width: 100%;
  margin: auto;
  text-align: center;
  font-family: arial;
  margin-top: 50px;
  //   background-image: url("https://source.unsplash.com/user/erondu/1600x600");
  background-repeat: no-repeat;
  background-size: cover;
  height: 481px;
}
</style>
