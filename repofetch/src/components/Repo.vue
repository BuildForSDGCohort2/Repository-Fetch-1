<template>
  <div class="main">
        <nav>
        <marquee behavior="slide" direction="up">
        <caption>Github Api Repository Fetcher</caption>
        </marquee>
        <div class="about">
        <router-link to="/about">About us</router-link>
        </div>
        </nav>
        <table :class="table">
        <tr>
        <th>ID</th>
        <th>Name</th>
        <th>URL</th>
        <th>Language</th>
        </tr>
        <tr v-for="repo in repos" :key="repo.id">
        <td>{{ repo.id }}</td>
        <td>{{ repo.name }}</td>
        <td>
        <router-link :to='`/about/${repo.id}`'>
        {{ repo.html_url }}
        </router-link>
        </td>
        <td>{{ repo.language }}</td>
      </tr>
        </table>
        <Pagination :data="{pageNumber}" />
    </div> 
</template>

<script>
import axios from 'axios';
import Pagination from '/Users/LENOVO/Repository-Fetch/repofetch/src/components/Pagination.vue'


    export default {
        name: 'repoSitory',
        components: {
            Pagination,
        },
        data() {
            return{
                repos: '',
                perPage: 5,
            }
        },
        created: function() {
        axios.get(`https://api.github.com/users/fabTimmy/repos?page=${this.pageNumber}&per_page=5`).then((response => {
          this.repos = response.data;
        }))
        },
      }
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Outfit&display=swap');
*{
  font-family: 'Outfit', sans-serif;
}
.links{
  text-decoration: none;
}
.about router-link{
  text-decoration: none;
}
.main{
  margin: auto;
}
table{
    color: #666;
    margin: 0 2rem;
    border: 2px solid #ccc;
    border-radius: 0.7rem;
    background: rgb(245, 248, 248);

}
th{
    background: #1c64ac;
    color: #fff;
    font-weight: 600;
    font-size: 1.2rem;
    text-align: center;
}
th, td{
    border: 1px solid #ccc;
    padding: 0.7rem 1.4rem;
}
caption{
    text-align: center !important;
    margin-top: 1rem;
    margin-left: 7rem;
    margin-bottom: 1rem;
    font-weight: 600;
    font-size: 1.7rem;
    white-space: nowrap;
}
.about{
  margin-right: 3rem;
  text-decoration: none;
  white-space: nowrap;
}
nav{
  display: flex;
  flex-direction: row;
  justify-content: space-between !important;
  align-items: center;
  margin-top: 1rem;
  margin-bottom: 0.2rem;
}
</style>