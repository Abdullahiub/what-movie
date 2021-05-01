<template>
  <div class="home">
      <div class="featured-card">
          <router-link to="/title/tt6802400">
          <img src="https://www.indiewire.com/wp-content/uploads/2020/12/coming-2-america.png?w=780" alt="Coming 2 America poster" class="featured-img">
          <div class="detail">
            <h3>Coming 2 America</h3>
            <p>The African monarch Akeem learns he has a long-lost son in the United States and must return to 
              America to meet this unexpected heir and build a relationship with his son.</p>
          </div>
          </router-link>
      </div>
      <form @submit.prevent="searchMovies()" class="search-box">
        <input type="text" placeholder="What Movie?" v-model="search" />
        <input type="submit" value="Go" />
      </form>

      <div class="movies-list">
        <div class="movie" v-for="movie in movies" :key="movie.imdbID">
          <router-link :to="'/title/' + movie.imdbID" class="movie-link">
              <div class="product-image">
                <img :src="movie.Poster" alt="Movie Poster" />
                <div class="type">{{ movie.Type }}</div>
              </div>
              <div class="detail">
                <p class="year">{{ movie.Year }}</p>
                <h3>{{ movie.Title }}</h3>
              </div>
          </router-link>
        </div>
      </div>
  </div>
</template>

<script>
import { ref } from 'vue';
import env from '@/env.js';
export default {
  setup () {
    const search = ref("");
    const movies = ref([]);

    const searchMovies = () => {
      if(search.value != "") {
        fetch(`http://www.omdbapi.com/?apikey=${env.apiKey}&s=${search.value}`)
        .then(response => response.json())
        .then(data => {
          movies.value = data.Search;
          search.value = "";
        });
      }
    }
    return {
      search,
      movies,
      searchMovies
    }
  }
}
</script>

<style>
  .home .featured-card {
    position: relative;
  }

  .home .featured-card .featured-img {
    display: block;
    width: 100%;
    height: 300px;
    object-fit: cover;
    position: relative;
    z-index: 0;
  }

  .home .featured-card .detail {
    position: absolute;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: rgba(0, 0, 0, 0.6);
    padding: 16px;
    z-index: 1;
  }

  .home .featured-card .detail h3 {
    color: #fff;
    margin-bottom: 16px;
  }

  .home .featured-card .detail p {
    color: #fff;
  }

  .home .search-box {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 16px;
  }

  .home .search-box input {
    display: block;
    appearance: none;
    border: none;
    outline: none;
    background: none;
  }

  .home .search-box input[type="text"]{
    width: 100%;
    color: #fff;
    background-color: #496583;
    font-size: 20px;
    padding: 10px 16px;
    border-radius: 8px;
    margin-bottom: 15px;
    transition: 0.4s;
  }

  .home .search-box input[type="text"]::placeholder{
    color: #f3f3f3;
  }

.home .search-box input[type="text"]:focus{
  box-shadow: 0px 3px 6px rgba(0, 0, 0, 0.2);
}

.home .search-box input[type="submit"]{
  width: 100%;
  max-width: 300px;
  background-color: #8b0000;
  padding: 16px;
  border-radius: 8px;
  color: #fff;
  font-size: 20px;
  text-transform: uppercase;
  transition: 0.4s;
}

.home .search-box input[type="submit"]:active {
  background-color: #8b0000;
}

.home .movies-list {
  display: flex;
  flex-wrap: wrap;
  margin: 0px 8px;
}

.home .movies-list .movie {
  max-width: 50%;
  flex: 1 1 50%;
  padding: 16px 8px;
}

.home .movies-list .movie .movie-link {
  display: flex;
  flex-direction: column;
  height: 100%;
}

.home .movies-list .movie .movie-link .product-image {
  position: relative;
  display: block;
}

.home .movies-list .movie .movie-link .product-image img {
  display: block;
  width: 100%;
  height: 275px;
  object-fit: cover;
}

.home .movies-list .movie .movie-link .product-image .type {
  position: absolute;
  padding: 8px 16px;
  background-color: #8b0000;
  color: #fff;
  bottom: 16px;
  left: 0px;
  text-transform: capitalize;
}

.home .movies-list .movie .movie-link .detail{
  background-color: #496583;
  padding: 16px 8px;
  flex: 1 1 100%;
  border-radius: 0px 0px 8px 8px;
}

.home .movies-list .movie .movie-link .detail .year {
  color: #aaa;
  font-size: 14px;
}

.home .movies-list .movie .movie-link .detail h3 {
  color: #fff;
  font-weight: 600;
  font-size: 18px;
}
</style>