
   <template>
    <div >
      <div class="mt-6">
        <div class="bg-gray-300 flex flex-col items-center justify-center">
          <nav class="bg-transparent p-4 shadow-md w-full">
            <ul class="flex justify-center space-x-8 text-amber-900 font-bold">
              <li>
                <a href="#" @click.prevent="fetchData('popular')" class="hover:text-gray-800">Popular</a>
              </li>
              <li>
                <a href="#" @click.prevent="fetchData('top_rated')" class="hover:text-gray-800">Top Rated</a>
              </li>
            </ul>
          </nav>
        </div>
  
        <div class="bg-gray-100 p-6">
          <h1 class="text-4xl font-bold text-amber-600 text-center m-8">{{ title }}</h1>
  
          <div class="grid grid-cols-1 md:grid-cols-3 lg:grid-cols-4 gap-6">
            <div 
              v-for="movie in movies" 
              :key="movie.id" 
              @click="showMovieDetails(movie)" 
              class="mx-4 group cursor-pointer sm:hover:shadow-slate-400 sm:shadow-md rounded-lg sm:border sm:border-amber-900 transition-shadow sm:m-2 duration-200 my-5 hover:translate-y-1 overflow-hidden shadow-black shadow-2xl bg-black dark:bg-amber-100"
            >
              <img :src="`https://image.tmdb.org/t/p/original/${movie.poster_path}`" 
                   alt="Movie Poster" 
                   class="w-fit object-cover">
              <div class="p-4">
                <h2 class="text-xl font-bold text-amber-900">{{ movie.title }}</h2>
                <p class="text-gray-900 text-xs font-bold mt-2">{{ movie.release_date }}</p>
                <p class="text-gray-900 text-xs font-bold mt-2"> 
                  <i class="fas fa-thumbs-up"></i>
                  {{ movie.vote_count }}
                </p>
              </div>
            </div>
          </div>
        </div>
      </div>
  
      <div>
    
    <div v-if="showDetails" class="fixed inset-0 bg-black bg-opacity-75 flex items-center justify-center z-50">
      <div class="bg-amber-100 p-6 rounded-lg shadow-lg max-w-lg w-full relative">
  
        <button @click="hideMovieDetails" class="absolute top-1 font-bold text-amber-900 right-2 text-2xl cursor-pointer" aria-label="Close">&times;</button>

        <div class="flex flex-col md:flex-row items-start">
       
          <img :src="`https://image.tmdb.org/t/p/original/${selectedMovie.poster_path}`" alt="Movie Poster" class="object-cover mt-4 md:mt-0 md:mr-4" width="200" height="200">

         
          <div class="flex-1">
            <h2 class="text-2xl text-amber-900 font-bold">{{ selectedMovie.title }}</h2>
            <p class="text-gray-800 text-sm  font-bold mt-4">{{ selectedMovie.overview }}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    name: 'Home',
    data() {
      return {
        movies: [],
        title: 'Popular Movies',
        showDetails: false,
        selectedMovie: null,
      };
    },
    mounted() {
      this.fetchData('popular'); 
    },
    methods: {
      async fetchData(category) {
        try {
          const response = await axios.get(
            `https://api.themoviedb.org/3/movie/${category}?api_key=c474edfe3c95519bc723dc7f6adab33f`
          );
          this.movies = response.data.results;
          this.title = category === 'popular' ? 'Popular Movies' : 'Top Rated Movies'; 
        } catch (error) {
          console.error('Error fetching data:', error);
        }
      },
      showMovieDetails(movie) {
        this.selectedMovie = movie;
        this.showDetails = true;
      },
      hideMovieDetails() {
        this.selectedMovie = null;
        this.showDetails = false;
      }
    },
  };
  </script>
  
  <style scoped>
 
  </style>
  