<template>
  <div class="root">
    <p v-if="loading">Loading...</p>
    <div class="location" v-for="location in locations" :key="location.id">
      <div class="location-image">
        <img :src="location.img_url" :alt="location.name" />
      </div>
      <div class="location-desc">
        <div class="location-title">{{ location.name }}</div>
        <div class="location-type">{{ location.type }}</div>
      </div>
      <div class="location-inhabitants">
        <span v-if="location.inhabitants.length == 0" class="none"
          >No inhabitants</span
        >
        <span
          v-else
          v-for="(inhabitant, index) in location.inhabitants"
          :key="inhabitant"
        >
          <span v-if="index == location.inhabitants.length - 1">{{
            inhabitant
          }}</span>
          <span v-else>{{ inhabitant }} <span class="spd">|</span></span>
        </span>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "Location",
  data() {
    return {
      locations: [],
      loading: false,
    };
  },
  created() {
    this.getLocations();
  },
  methods: {
    getLocations() {
      this.loading = true;
      fetch("https://finalspaceapi.com/api/v0/location/?limit=3")
        .then((res) => res.json())
        .then((data) => (this.locations = data));
      this.loading = false;
    },
  },
};
</script>
<style scoped>
.root {
  margin: 0 auto;
  padding: 0 10px;
  font-family: sans-serif;
  font-weight: 300;
  display: flex;
  justify-content: space-around;
  flex-direction: column;
  align-items: center;
  color: purple;
}
.location {
  box-shadow: 0 5px 8px 0 rgba(0, 0, 0, 0.3);
  padding: 12px;
  margin-bottom: 10px;
  text-align: center;
  width: 18rem;
  background-color: #fafafa;
  margin-bottom: 15px;
  border-radius: 7px;
}
.location-desc {
  display: flex;
  justify-content: space-between;
}
.location-image img {
  width: 100%;
  height: calc(16rem - 12px);
  border-radius: 7px;
  margin-bottom: 10px;
}
.location-title {
  font-size: "1.1rem";
  font-weight: 400;
}
.location-type {
  color: rgb(107, 107, 107);
  font-size: 0.9rem;
}
.location-inhabitants {
  color: rgb(107, 107, 107);
  text-align: left;
  font-size: 0.9rem;
  margin: 0.7rem 0;
}
.location-inhabitants span {
  margin: 0 0.1rem;
}
.spd {
  font-size: 1.1rem;
  font-weight: 200;
  color: rgb(223, 223, 223);
}
</style>