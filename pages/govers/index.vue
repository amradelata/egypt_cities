<template>
  <div>
    <mynav />
    <div class="cards">
      <div class="card" v-for="cities in govremtes" :key="cities.id">
        <nuxt-link :to="'govers/' + cities.id">
          <div class="img" :style="{ backgroundImage: 'url(' + cities.img + ')' }"></div>
          <div class="content">
            <h4>{{cities.ar_name}}</h4>
          </div>
        </nuxt-link>
      </div>
    </div>
  </div>
</template>

<script>
import mynav from "~/components/mynav.vue";
import axios from "axios";
const covers = "https://egypt-database.herokuapp.com/governorates";
export default {
  components: {
    mynav
  },
  data() {
    return {
      govremtes: []
    };
  },
  async created() {
    const res = await axios.get(covers);
    this.govremtes = res.data;
    console.log(this.govremtes);
  }
};
</script>


<style scoped>
.governorates {
  margin-bottom: 100px;
}
.field {
  margin-top: 50px;
}
.dad {
  font-family: "Cairo", sans-serif;
  text-align: right;
  display: block;
}
h4 {
  text-align: center;
}
.chiled {
  font-size: 1.5em;
}

.cards {
  display: flex;
  flex-wrap: wrap;
  margin-top: 50px;
}
.card {
  flex-basis: calc(25% - 20px);
  display: inline-block;
  background-color: #fff;
  box-shadow: 0 3px 6px rgba(0, 0, 0, 0.16), 0 3px 6px rgba(0, 0, 0, 0.23);
  margin: 10px;
  border-radius: 4px;
  padding: 0;
  overflow: hidden;
  margin: auto;
  margin-bottom: 50px;
  border: none;
}
.card .content {
  padding: 15px;
  color: #000;
}
.img {
  height: 190px;
  width: 100%;
  background-size: contain;
  background-position: center center;
  background-repeat: no-repeat;
}
@media screen and (max-width: 768px) {
  .card {
    flex-basis: calc(100% - 20px);
  }
}
</style>