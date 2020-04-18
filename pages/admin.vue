<template>
  <div id="admin">
    <section class="hero is-primary">
      <div class="hero-body">
        <div class="container">
          <h1 class="title">صفحه العرض والتحكم</h1>
        </div>
      </div>
    </section>

    <div class="container">
      <div class="field has-addons">
        <div class="control">
          <input
            class="input is-primary"
            type="text"
            placeholder="add governorate"
            v-model="governValue"
            @keyup.enter="addGovern"
          />
        </div>
        <p class="control">
          <button class="myRtlButton" @click="addGovern">add</button>
        </p>
      </div>

      <ul v-for="(city,index) in governorates" class="subtitle box" :key="city.id">
        <router-link v-bind:to="'/citiesadmin/' + city.id">
          <span :id="city.id" ref="span">{{city.ar_name}}</span>
        </router-link>
        <div class="buttons">
          <button
            @click="edit(index)"
            :style="{'display': change}"
            class="button is-link"
            ref="edit"
            id="edit"
          >edit</button>
          <input
            class="input is-success"
            type="text"
            :style="{'display': input}"
            :value="city.ar_name"
            ref="input"
            id="input"
          />
          <button
            @click="remov(index = city.id)"
            :style="{'display': delet}"
            class="button is-danger"
            ref="delete"
            id="delete"
          >delete</button>
          <button
            @click="save(index)"
            :style="{'display': saveChang}"
            class="button is-success"
            ref="save"
            id="save"
          >save</button>
        </div>
      </ul>
    </div>
  </div>
</template>

<script>
import axios from "axios";
const citiesData = "https://egypt-database.herokuapp.com/cities";
const governoratesData = "https://egypt-database.herokuapp.com/governorates";
export default {
  data() {
    return {
      cities: [],
      governorates: [],
      searchVale: "",
      governValue: "",
      saveChang: "none",
      input: "none",
      change: "inline-block",
      delet: "inline-block",
      inputChang: ""
    };
  },
  methods: {
    async search(index) {
      const myID = this.governorates[index].id;
      const res = await axios.get(citiesData + "/" + "?governorate_id=" + myID);
      this.cities = res.data;
    },
    async addGovern() {
      const res = await axios.post(governoratesData, {
        ar_name: this.governValue,
        img:
          "https://aliceasmartialarts.com/wp-content/uploads/2017/04/default-image.jpg"
      });
      this.governorates.push(res.data);
      this.governValue = "";
    },
    async remov(index) {
      console.log(this.governorates.length);

      const res = await axios.delete(governoratesData + "/" + index);
      const dele = await axios.get(governoratesData);
      this.governorates = dele.data;

      console.log(dele.data.length);
    },
    edit(index) {
      console.log(index);
      const input = this.$refs["input"][index];
      const edit = this.$refs["edit"][index];
      const delet = this.$refs["delete"][index];
      const save = this.$refs["save"][index];

      edit.style.display = "none";
      delet.style.display = "none";
      save.style.display = "inline-block";
      input.style.display = "inline-block";
    },

    async save(index) {
      console.log(index);
      const inputValue = this.$refs["input"][index].value;
      const input = this.$refs["input"][index];
      const edit = this.$refs["edit"][index];
      const delet = this.$refs["delete"][index];
      const save = this.$refs["save"][index];
      const span = this.$refs["span"][index].id;

      edit.style.display = "inline-block";
      delet.style.display = "inline-block";
      save.style.display = "none";
      input.style.display = "none";
      console.log(inputValue);

      const res = await axios.patch(governoratesData + "/" + span, {
        ar_name: inputValue
      });
      const edi = await axios.get(governoratesData);
      this.governorates = edi.data;
    }
  },
  async created() {
    const res = await axios.get(governoratesData);
    this.governorates = res.data;
  }
};
</script>

<style scoped>
#admin {
  direction: rtl;
  position: relative;
}

section {
  margin-bottom: 50px;
}
ul {
  width: 45vw;
  display: inline-block;
}
.input {
  width: 40vw;
}
.mybox {
  background-color: white;
  border-radius: 6px;
  box-shadow: 0 2px 3px rgba(10, 10, 10, 0.1), 0 0 0 1px rgba(10, 10, 10, 0.1);
  color: #4a4a4a;
  display: block;
  padding: 5px;
}
.menu {
  position: absolute;
  left: 0;
  text-align: left;
  top: 0;
  display: inline-block;
}
.menu ul {
  width: 20vw;
}
.myRtlButton {
  border-bottom-left-radius: 10px;
  border-top-left-radius: 10px;
  border-bottom-right-radius: 0;
  border-top-right-radius: 0;
  background-color: white;
  border-color: #00d1b2;
  border-width: 1px;
  color: #363636;
  cursor: pointer;
  justify-content: center;
  padding: 8px;
  margin-right: 3px;
  text-align: center;
  white-space: nowrap;
  padding: 10px;
}
.buttons {
  margin-top: 20px;
}
@media screen and (max-width: 768px) {
  input {
    margin-right: 20px;
  }
}
</style>
