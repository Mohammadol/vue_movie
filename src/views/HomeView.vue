<template>
  <div class="home">
    <div class="feature-card">
      <router-link to="/movie/tt0409591">
        <img
          src="https://m.media-amazon.com/images/M/MV5BMTQ5MTcyNDYwMV5BMl5BanBnXkFtZTgwNzMzNzc0MjE@._V1_SX300.jpg"
          alt="coffe"
          class="featured-img"
        />
        <div class="details">
          <h3>Movies</h3>
          <p>
            You can search movies or series anime or Whatever you want, Ihope
            you enjoy taking this journy on my test responsive web site and take
            look for this work.
          </p>
        </div>
      </router-link>
    </div>
    <form @submit.prevent="ok" class="search-box">
      <input
        type="text"
        placeholder="What are you looking for?"
        v-model="search"
      />
      <input type="submit" value="search" />
    </form>
    <div class="movies-list">
      <div class="movie" v-for="movie in Movies" :key="movie.imdbID">
        <router-link :to="`/movie/${movie.imdbID}`" class="movie-link">
          <div class="product-image">
            <img :src="movie.Poster" alt="movieposter" />
            <div class="type">{{ movie.Type }}</div>
          </div>
          <div class="details">
            <p class="year">{{ movie.Year }}</p>
            <h3 class="">{{ movie.Title }}</h3>
          </div>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
import env from "@/env.js";
export default {
  setup() {
    const search = ref("");
    const Movies = ref([]);
    const ok = () => {
      if (search.value != "") {
        fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&s=${search.value}`)
          .then((response) => response.json())
          .then((data) => {
            Movies.value = data.Search;
            search.value = "";
            console.log(Movies.value);
          })
          .catch((err) => {
            console.log(err);
          });
      }
    };
    return { search, ok, Movies };
  },
};
</script>
<style lang="scss">
.home {
  .feature-card {
    width: 70%;
    margin: auto;
    position: relative;

    .featured-img {
      display: block;
      width: 100%;
      height: 500px;
      object-fit: cover;

      z-index: 0;
    }
    .details {
      position: absolute;
      right: 0;
      left: 0;
      bottom: 0;
      width: 100%;
      background-color: rgb(0, 0, 0, 0.6);
      padding: 16px;
      z-index: 1;
      h3 {
        color: #fff;
        margin-bottom: 16px;
      }
      p {
        color: #fff;
      }
    }
  }
  .search-box {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 16px;
    width: 70%;
    margin: auto;
    input {
      display: block;
      appearance: none;
      border: none;
      outline: none;
      background: none;
      &[type="text"] {
        width: 100%;
        color: #fff;
        background-color: #496583;
        font-size: 20px;
        padding: 10px;
        border-radius: 8px;
        margin-bottom: 16px;
        transition: 0.4s;
        &::placeholder {
          color: #f3f3f3;
        }
        &:focus {
          box-shadow: 0px 3px 6px rgb(0, 0, 0, 0.2);
        }
      }
      &[type="submit"] {
        width: 100%;
        max-width: 300px;
        background-color: #42b883;
        padding: 16px;
        border-radius: 8px;
        color: white;
        font-size: 20px;
        text-transform: uppercase;
        transition: 0.4s;
        &:active {
          background-color: #3b8070;
        }
      }
    }
  }
  .movies-list {
    display: flex;
    flex-wrap: wrap;
    margin: 0px 8px;
    .movie {
      @media screen and (max-width: 560px) {
        max-width: 50%;
        flex: 1 1 50%;
        padding: 16px 8px;
      }
      @media screen and (max-width: 720px) and (min-width: 561px) {
        max-width: 33.333333333%;
        flex: 1 1 33.333333333%;
        padding: 16px 8px;
      }
      @media screen and (max-width: 1200px) and (min-width: 721px) {
        max-width: 25%;
        flex: 1 1 25%;
        padding: 16px 8px;
      }
      @media screen and (max-width: 1620px) and (min-width: 1201px) {
        max-width: 20%;
        flex: 1 1 20%;
        padding: 16px 8px;
      }
      @media screen and (max-width: 1920px) and (min-width: 1621px) {
        max-width: 16.666666667%;
        flex: 1 1 16.666666667%;
        padding: 16px 8px;
      }

      .movie-link {
        display: flex;
        flex-direction: column;
        height: 100%;
        .product-image {
          position: relative;
          display: block;
          border-radius: 8px 8px 0px 0px;
          img {
            display: block;
            width: 100%;
            height: 275px;
            object-fit: cover;
            border-radius: 8px;
          }
          .type {
            position: absolute;
            text-transform: capitalize;
            padding: 8px 16px;
            background-color: #42b883;
            color: #fff;
            bottom: 16px;
            left: 0px;
          }
        }
        .details {
          background-color: #496583;
          padding: 16px 8px;
          flex: 1 1 100%;
          border-radius: 0px 0px 8px 8px;
        }
        .year {
          color: #aaa;
          font-size: 14px;
        }
        h3 {
          color: #fff;
          font-weight: 600;
          font-size: 17px;
        }
      }
    }
  }
}
</style>
