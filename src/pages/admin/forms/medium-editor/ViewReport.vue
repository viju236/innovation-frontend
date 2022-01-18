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
              <option v-for="(value, key) in devTeams" :key="key">
                {{ value.description }}
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
              <option v-for="(value, key) in scrumTeams" :key="key">
                {{ value.name }}
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
              <option v-for="(value, key) in managerName" :key="key">
                {{ value.name }}
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
      </div>
    </div>
  </div>
</template>
 <script>
export default {
  name: "ViewReport",
  data() {
    return {
      SelecteddevTeams: [],
      SelectedscrumTeams: [],
      SelectedTeam: [],
      SelectedLocations: [],
      SelectedManager: [],
      selected: "A",
      devTeam: "",
      devTeams: [
        {
          id: 1,
          description: "Team 1",
        },
        {
          id: 2,
          description: "Team 2",
        },
        {
          id: 3,
          description: "Team 3",
        },
      ],
      scrumTeams: [
        {
          id: 1,
          name: "Simple Minds",
        },
        {
          id: 2,
          name: "Avengers",
        },
        {
          id: 3,
          name: "KFP",
        },
      ],
      Options: [
        {
          id: 1,
          name: "Cloud",
        },
        {
          id: 2,
          name: "Desktop",
        },
      ],
      Locations: [
        {
          id: 1,
          name: "Pune",
        },
        {
          id: 2,
          name: "HST",
        },
      ],
      managerName: [
        {
          id: 1,
          name: "Ninad Kulkarni",
        },
        {
          id: 2,
          name: "Rahul Kulkarni",
        },
      ],
    };
  },
  methods: {
    submitData() {
      console.log("in function----", this.devTeam);
      console.log("SelectedscrumTeams---", this.SelectedscrumTeams);
      //   console.log('SelectedTeam---',SelectedTeam);
      //    console.log('SelectedLocations---',SelectedLocations);
      //     console.log('SelectedManager---',SelectedManager);
    },
  },
};
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
  background-color: rgb(233, 232, 232);
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
