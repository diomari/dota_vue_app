<template>
  <div class="team">
    <h1>This is {{team.name}} page</h1>
    <h2>Matches:</h2>
    <li v-for="match in matches" :key="match.id">
        {{match.id}}
        <br> {{match.league_name}}
        <br> {{match.duration}}
    </li>
    {{matches}}
  </div>
</template>
<script>
export default {
    data () {
        return {
            matches: [],
            team: {}
        }
    },
    mounted () {
        const api_url = 'https://api.opendota.com/api';
        // get team
        axios.get(`${api_url}/teams/${this.$route.params.id}/`).then(response => {
            this.team = response.data;
        })
        // get matches
        axios.get(`${api_url}/teams/${this.$route.params.id}/matches/`).then(response => {
            this.matches = response.data;
        })
    }
}
</script>
