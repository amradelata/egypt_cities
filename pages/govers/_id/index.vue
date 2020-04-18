<template>
  <div>
    <mynav />
    <div>
      <div class="singleBage container">
        <div class="cards">
          <div class="card" v-for="citie in citiesBranch" :key="citie.id">
            <div class="content">{{citie.ar_name}}</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import mynav from "~/components/mynav.vue";
const citiesData = "https://egypt-database.herokuapp.com/cities";
export default {
  components: {
    mynav
  },
  data() {
    return {
      id: this.$route.params.id,
      citiesBranch: []
    };
  },
  async created() {
    const res = await axios.get(citiesData + "/?governorate_id=" + this.id);
    this.citiesBranch = res.data;
    console.log(this.id);
    // console.log(this.citiesBranch);
  }
};
</script>
<style scoped>
.singleBage {
  padding: 100px 0;
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
}
.card .content {
  padding: 15px;
  color: #000;
  text-align: center;
  font-size: 2em;
}

.card:first-child {
  background: #6a89cc;
}
@media screen and (max-width: 768px) {
  .card {
    flex-basis: calc(100% - 20px);
  }
}
</style>
