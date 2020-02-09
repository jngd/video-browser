<template>
  <div>
    <SearchBar @termChange="onTermChange"></SearchBar>
    <VideoList></VideoList>
    {{ videos.length }}
  </div>
</template>

<script>
import axios from 'axios';
import SearchBar from './components/SearchBar';
import VideoList from './components/VideoList';
// TODO: Use your own
const API_KEY = '';

export default {
  name: 'App',
  components: {
    SearchBar,
    VideoList,
  },
  data() {
    return { videos: [] };
  },
  methods: {
    onTermChange(searchTerm) {
      console.log(searchTerm);
      axios
        .get('https://www.googleapis.com/youtube/v3/search', {
          params: {
            key: API_KEY,
            type: 'video',
            part: 'snippet',
            q: searchTerm,
          },
        })
        .then((response) => {
          // Updating data.videos !!!
          console.log('ADDING VIDEOS');
          this.videos = response.data.items;
        });
    },
  },
};
</script>
