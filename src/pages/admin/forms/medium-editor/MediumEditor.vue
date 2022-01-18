<template>
  <div class="medium-editor">
    <div class="header-control">
      <h1 class="header">Week - {{ getMondayDate }}</h1>
      <div class="image-control">
        <img class="imagePreview" :src="previewImage" alt="DP" />
        <input type="file" accept="image/jpeg" @change=uploadImage>
      </div>
      <h1>Status Report :</h1>
    </div>
    <div class="editor-control">
      <QuillEditor theme="snow" />
    </div>
    <div class="container">
      <label class="label-control" for="Name">User Name:</label>
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
      <span>Enter user name. eg. Rishikesh Dhobale</span>
      <label class="label-control" for="ScrumTeam">Scrum Team:</label>
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
      <span>Enter scrum team name. eg. Avengers</span>
      <label for="DevTeam">Development Team:</label>
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
      <span>Enter development team name. eg. SE IND DEV1</span>
      <label for="Domain">Desktop/Cloud:</label>
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
      <span>Enter domain name. eg. Desktop or Cloud</span>
      <label for="Location">Pune/HSV:</label>
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
      <span>Enter location. eg. Pune or Huntsville</span>
      <label for="ManagerName">Manager Name:</label>
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
      <span>Enter manager name. First name and last name eg. Ninad Kulkarni</span>
      <label for="AdditionalTag">Additional Tags:</label>
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
      <span>Enter comma seperated additional tags. eg. vue.js, javascript, cpp</span>
    </div>
    <!-- <div class="row">
      <div class="flex md12">
        <div class="row">
          <va-input
            v-model="userName"
            label="User Name"
          >
          </va-input>
          <va-input
            v-model="nextFriday"
            label="Date"
          >
          </va-input>
        </div>
        <va-card>
          <va-card-title>{{ $t("forms.mediumEditor.title") }}</va-card-title>
          <va-card-content class="d-flex flex-center">
            <va-medium-editor @initialized="handleEditorInitialization">
              <h1>Select Text To Open Editor</h1>

              <p>
                You enter into your favorite local bar looking
                <span class="default-selection"><b>good</b></span> as hell, but
                you know the only heads you want to turn—spicy & stylish alpha
                bitches — are heavily fixated on the D. The hot girl talks to
                you, but she only wants to be your best friend. Her
                nonthreatening and attentive best friend. Receiver of sexy
                selfies, listener of stories. Meanwhile, you attract unwanted
                attention from straight men, pudgy and greasy moths to your
                emotionally distant flame.
              </p>

              <p>
                Read the full article on
                <a
                  href="https://medium.com/@dorn.anna/girl-no-you-dont-2e21e826c62c"
                >Medium</a
                >
              </p>
            </va-medium-editor>
          </va-card-content>
        </va-card>
        <div class="flex md6 xs12">
          <label>Dev Team:</label>
          <input type="text" class="input-control" name="devTeam" v-model="input.name" />
          <label>Scrum Team:</label>
          <input type="text"/>
          <label>Desktop/Cloud:</label>
          <input type="text"/>
          <label>Pune/HSV:</label>
          <input type="text"/>
          <label>Manager:</label>
          <input type="text"/>
          <va-select
            label="Dev Team"
            v-model="devTeam"
            textBy="description"
            track-by="id"
            :options="devTeams"
          />
          <va-select
            label="Scrum Team"
            v-model="scrumTeam"
            textBy="description"
            track-by="id"
            :options="scrumTeams"
          />
          <va-select
            label="Desktop/Cloud"
            v-model="desktopOrCloud"
            textBy="description"
            track-by="id"
            :options="desktopCloud"
          />
          <va-select
            label="Pune/HSV"
            v-model="location"
            textBy="description"
            track-by="id"
            :options="locations"
          />
          <va-select
            label="Manager"
            v-model="manager"
            textBy="description"
            track-by="id"
            :options="managers"
          />
        </div>
      </div>
    </div> -->
  </div>
</template>

<script>
// import VaMediumEditor from "@/components/va-medium-editor/va-medium-editor";
// import axios from "axios";
import { QuillEditor } from '@vueup/vue-quill'
import '@vueup/vue-quill/dist/vue-quill.snow.css';

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
      previewImage: './profile_photo.jpg',
      userNames: [
        'Rishikesh','Kshitij','Abhijit'
      ],
      scrumTeamNames: ['Avegers', 'Autobots'],
      devTeamNames: [],
      domainNames: [],
      locationNames: [],
      managerNames: [],
      additionTags: []
    };
  },

  computed: {
    getMondayDate() {
      // const monday = new Date();
      // monday.setDate(
      //   monday.getDate() + ((((7 - monday.getDay()) % 7) + 1) % 7)
      // );
      // return monday.toDateString();
      const today = new Date();
      const day = today.getDay() || 7; // Get current day number, converting Sun. to 7
      // Only manipulate the date if it isn't Mon.
      if( day !== 1 ) {
        today.setHours(-24 * (day - 1));
      }            
      return today.toDateString();
    },
  },

  methods: {
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
  },
};
</script>
<style lang="scss">
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
  grid-template-columns: 135px auto auto;
  // grid-template-columns: repeat(3, auto);
  align-items: center;
}

.imagePreview{
  width: 100px;
  height: 100px;
  margin-right: 20px;
}

.editor-control{
  margin-top: 30px;
  height: 300px;
}

.image-control{
  position: relative;
  text-align: end;
}

.header-control{
  display: grid;
  grid-template-columns: auto auto;
}
</style>
