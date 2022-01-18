<template>
  <div class="medium-editor">
  <div style= "padding-left: 700px;">
      <button class="button" @click="submitData">Save Changes</button>
    </div>
    <div class="header-control">
      <h1 class="header">Week - {{ getMondayDate }}</h1>

      <div class="image-control">
        <img class="imagePreview" :src="previewImage" alt="DP" />
        <label for="files"><b>Select Image</b></label>
        <input type="file" id="files" style="visibility:hidden;" accept="image/jpeg" @change=uploadImage>
      </div>
    </div>
    <h1>Status Report -</h1>
    <div class="editor-control">
      <QuillEditor 
        ref="myQuillEditor"
        v-model="content"
        @ready="onEditorReady($event)"
        @change="onEditorChange($event)"
        theme="snow" />
    </div>
    <div class="container">
      <label class="label-control" for="Name"><b>User Name:</b></label>
      <input
        type="text"
        class="input-control"
        id="Name"
        list="NameList"
        v-model="userName"
      />
      <datalist id="NameList">
        <option v-for="(value, key) in userNames" :key="key">
          {{ value }}
        </option>
      </datalist>
      <span><i><b>Enter user name. eg. Rishikesh Dhobale</b></i></span>
      <label class="label-control" for="ScrumTeam"><b>Scrum Team:</b></label>
      <input
        type="text"
        class="input-control"
        id="ScrumTeam"
        list="ScrumTeamList"
        v-model="scrumTeam"
      />
      <datalist id="ScrumTeamList">
        <option v-for="(value, key) in scrumTeamNames" :key="key">
          {{ value }}
        </option>
      </datalist>
      <span><i><b>Enter scrum team name. eg. Avengers</b></i></span>
      <label for="DevTeam"><b>Development Team:</b></label>
      <input
        type="text"
        class="input-control"
        id="DevTeam"
        list="DevTeamList"
        v-model="devTeam"
      />
      <datalist id="DevTeamList">
        <option v-for="(value, key) in devTeamNames" :key="key">
          {{ value }}
        </option>
      </datalist>
      <span><i><b>Enter development team name. eg. SE IND DEV1</b></i></span>
      <label for="Domain"><b>Desktop/Cloud:</b></label>
      <input
        type="text"
        class="input-control"
        id="Domain"
        list="DomainList"
        v-model="domain"
      />
      <datalist id="DomainList">
        <option v-for="(value, key) in domainNames" :key="key">
          {{ value }}
        </option>
      </datalist>
      <span><i><b>Enter domain name. eg. Desktop or Cloud</b></i></span>
      <label for="Location"><b>Pune/HSV:</b></label>
      <input
        type="text"
        class="input-control"
        id="Location"
        list="LocationList"
        v-model="location"
      />
      <datalist id="LocationList">
        <option v-for="(value, key) in locationNames" :key="key">
          {{ value }}
        </option>
      </datalist>
      <span><i><b>Enter location. eg. Pune or Huntsville</b></i></span>
      <label for="ManagerName"><b>Manager Name:</b></label>
      <input
        type="text"
        class="input-control"
        id="ManagerName"
        list="ManagerList"
        v-model="managerName"
      />
      <datalist id="ManagerList">
        <option v-for="(value, key) in managerNames" :key="key">
          {{ value }}
        </option>
      </datalist>
      <span><i><b>Enter manager name. First name and last name eg. Ninad Kulkarni</b></i></span>
      <label for="AdditionalTag"><b>Additional Tags:</b></label>
      <input
        type="text"
        class="input-control"
        id="AdditionalTag"
        list="AdditionalTagList"
        v-model="tags"
      />
      <datalist id="AdditionalTagList">
        <option v-for="(value, key) in additionTags" :key="key">
          {{ value }}
        </option>
      </datalist>
      <span><i><b>Enter comma seperated additional tags. eg. vue.js, javascript, cpp</b></i></span>
    </div>
    
  </div>
</template>

<script>

// import VaMediumEditor from "@/components/va-medium-editor/va-medium-editor";
// import axios from "axios";
import { QuillEditor, Quill } from '@vueup/vue-quill'
import '@vueup/vue-quill/dist/vue-quill.snow.css';
import axios from 'axios';
var quill = new Quill('#editor', {
    theme: 'snow'
});
export default {
  components: {
    QuillEditor
  },

  data() {
    return {
      devTeam: '',
      scrumTeam: '',
      location: '',
      managerName: '',
      userName: '',
      domain: '',
      tags: '',
      editor: '',
      previewImage: "file:///D:/Innovation2022/innovation-frontend/src/pages/admin/forms/medium-editor/profile_photo.jpg",
      userNames: [],
      scrumTeamNames: [],
      devTeamNames: [],
      domainNames: [],
      locationNames: [],
      managerNames: [],
      additionTags: [],
      content: '',
      //  quill : Quill

    };
  },

  computed: {

    getMondayDate() {
      const today = new Date();
      const day = today.getDay() || 7; // Get current day number, converting Sun. to 7
      if( day !== 1 ) {
        today.setHours(-24 * (day - 1));
      }            
      return today.toDateString();
    },
    editor() {
      console.log('this.$refs.myQuillEditor.quill----',this.$refs.myQuillEditor.quill);
      return this.$refs.myQuillEditor.quill
    }
  },

 mounted() {
      console.log('this is current quill instance object', this.editor);
      this.getUniqueFilters();
    },

  methods: {
    getUniqueFilters() {
      axios.get('http://localhost:3000/v1/users/getUniqueFilters').then(response => {
        this.scrumTeamNames = Object.freeze(response.data.scrumTeam);
        this.devTeamNames = Object.freeze(response.data.devTeam);
        this.managerNames = Object.freeze(response.data.manager);
      })
    },
     onEditorReady(quill) {
        console.log('editor ready!', quill)
        this.content = quill;
      },

    uploadImage(e){
        console.log(this.window);
        const image = e.target.files[0];
        const reader = new FileReader();
        reader.readAsDataURL(image);
        reader.onload = e =>{
            this.previewImage = e.target.result;
        };
    },
    handleEditorInitialization(editor) {
      this.editor = editor;
      this.$nextTick(() => {
        this.highlightSampleText();
      });
    },

    highlightSampleText() {
      const sampleText =
        document.getElementsByClassName("default-selection")[0];
      this.editor.selectElement(sampleText);
    },
    submitData(){
      // var editor_content = quill.container.innerHTML
      // console.log('text-----',Quill.getHTML());
      // console.log('document.getElementsByClassName-----',document.getElementsByClassName('ql-editor ql-blank'));
      // console.log('this.$refs.myQuillEditor.quill-----',this.$refs.myQuillEditor.quill);
       console.log('text1111-----',this.content.container.innerHTML);
      let data = {
        //img: this.previewImage,
        name: this.userName,
        scrumTeam: this.scrumTeam,
        devTeam: this.devTeam,
        teamType:this.domain,
        location: this.location,
        manager: this.managerName,
        tags: this.tags,
        reportContent: this.content.container.innerHTML,
      }
      axios.post('http://localhost:3000/v1/auth/register', data).then(response => 
      {
        console.log('response-----', response);
        this.clearAll();
        this.getUniqueFilters();
      });
      
    },
    clearAll() {
      this.devTeam =  '';
      this.scrumTeam =  '';
      this.location =  '';
      this.managerName =  '';
      this.userName = '';
      this.domain =  '';
      this.tags = '';
      this.editor = '';
      this.content =  '';
    }
  },
};
</script>
<style lang="scss">

// .medium-editor{
// background-image: url('report5.jpg');
// background-repeat: no-repeat;
//     background-size: cover;
// }
.header{
  font-size: 40px;
}

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
  grid-template-columns: 150px auto auto;
  // grid-template-columns: repeat(3, auto);
  align-items: center;
}

.imagePreview{
  width: 100px;
  height: 100px;
  margin-right: 20px;
}

.editor-control{
  margin-top: 5px;
  height: 300px;
  background-color: white;
}

.image-control{
  position: relative;
  text-align: end;
}

.header-control{
  display: grid;
  grid-template-columns: auto auto;
  margin-bottom: 10px;
}

.ql-toolbar.ql-snow + .ql-container.ql-snow {
background-color: white;
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
</style>
