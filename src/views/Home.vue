<template>
  <v-container fluid>
          <v-progress-circular
            indeterminate
            color="primary"
            v-show="isLoading"
          ></v-progress-circular>
      <v-layout v-show="!isLoading" column align-center>
        <v-list two-line>
          <template v-for="team in teams">
            <v-list-tile
              :key="team.ratings"
              avatar
              @click="getTeam(team.team_id)"
            >
              <v-list-tile-avatar>
                <v-icon v-html="'pages'"></v-icon>
              </v-list-tile-avatar>

              <v-list-tile-content>
                <v-list-tile-title v-html="team.name"></v-list-tile-title>
                <v-list-tile-sub-title >Wins: {{team.wins}}</v-list-tile-sub-title>
              </v-list-tile-content>
            </v-list-tile>
          </template>
        </v-list>
          <footer>
            <small>
              <em>&mdash;John Johnson</em>
            </small>
          </footer>
      </v-layout>
  </v-container>
</template>
<script>
export default {
  data () {
    return {
      teams: [],
      isLoading: true
    }
  },
  mounted () {
    const api_url = 'https://api.opendota.com/api';
    // get rankings from dota api
    axios.get(`${api_url}/teams`).then(response => {
      this.isLoading = false;
      this.teams = response.data;
      
    })
  },
  methods: {
    getTeam(team_id) {
      this.$router.push({name: 'team', params: {id: team_id}});
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
