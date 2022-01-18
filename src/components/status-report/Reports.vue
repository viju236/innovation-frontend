<template>
  <div class="reports">
    <div class="row">
      <div class="flex xs12">
        <va-card :title="$t('forms.selects.title')">
          <va-card-content>
            <form>
              <div class="row">
                <div class="flex md4 sm6 xs12">
                 <!--  <input type="text" class="input-control" id="ScrumTeam" list="devTeams" v-model="scrumTeam" />
                 <datalist id="devTeams">
                    <option v-for="(value, key) in devTeams" :key="key">
                      {{ value.description }}
                    </option>
                  </datalist> -->
                    <va-select :label="$t('forms.selects.devTeam')" v-model="multiSelectdevTeams" textBy="description"
                    track-by="id" multiple :options="devTeams" /> 
                </div>
                <div class="flex md4 sm6 xs12">
                  <va-select :label="$t('forms.selects.scrumTeam')" v-model="multiSelectscrumTeams" textBy="name"
                    track-by="id" multiple :options="scrumTeams" />
                </div>
                <div class="flex md4 sm6 xs12">
                  <va-select :label="$t('forms.selects.desktop')" v-model="multiSelectModel" textBy="name" track-by="id"
                    multiple :options="Options" />
                </div>
                <div class="flex md4 sm6 xs12">
                  <va-select :label="$t('forms.selects.location')" v-model="multiSelectLocations" textBy="name"
                    track-by="id" multiple :options="Locations" />
                </div>
                <div class="flex md4 sm6 xs12">
                  <va-select :label="$t('forms.selects.manager')" v-model="simpleSelectModel" textBy="description"
                    track-by="id" multiple :options="managerName" />
                </div>
                <va-button class="mr-2 mb-2" > {{ $t('buttons.submit') }}</va-button>
              </div>
            </form>
          </va-card-content>
        </va-card>
      </div>
    </div>
    <div class="cards">
    <div class="cards-container row d-flex wrap align--start">
    <div class="flex xs12">
          <va-card>
            <va-card-title>{{ $t('cards.title.statusReport') }}</va-card-title>
            <va-card-content>{{ $t('cards.statusText') }}</va-card-content>
          </va-card>
        </div>
    </div>
    </div>
  </div>
</template>
<script>
  export default {
    name: 'reports',
    data() {
      return {
        multiSelectdevTeams: [],
        multiSelectscrumTeams: [],
        multiSelectModel: [],
        multiSelectLocations: [],
        simpleSelectModel: '',
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
          },
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
        managerName: ''
      }
    }
  }
</script>