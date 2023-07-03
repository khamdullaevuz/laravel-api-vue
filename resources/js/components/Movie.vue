<template>
    <table>
        <tr>
            <th scope="col">ID</th>
            <th scope="col">Title</th>
            <th scope="col">Director</th>
        </tr>
        <tr v-for="movie in movies" :key="movie.id">
            <td>{{ movie.id }}</td>
            <td>{{ movie.title }}</td>
            <td>{{ movie.director }}</td>
        </tr>
    </table>
</template>

<script>
import axios from 'axios';
export default {
    data() {
        return {
            movies: []
        }
    },
    methods: {
        async getMovies() {
            await axios.get('/api/movies')
                .then(response => {
                    this.movies = response.data.data;
                })
                .catch(error => {
                    console.log(error);
                });
        }
    },
    mounted() {
        this.getMovies();
    }
}
</script>

<style scoped>
table {
    border-collapse: collapse;
    width: 100%;
}

th, td {
    text-align: left;
    padding: 8px;
}

tr:nth-child(even) {
    background-color: #f2f2f2;
}

th {
    background-color: #4CAF50;
    color: white;
}
</style>
