/* eslint-disable */
<template>
   <div class="hello">
        <div class="container p-5 my-5 bg-dark text-white">
            <h1>{{ msg }} </h1>
            <p>
                Below you can see the pictures taken of Earth this week.<br>
                These images was taken by NASA's EPIC camera onboard the NOAA DSCOVR spacecraft.
            </p>
     
        </div>
        <div v-for="(image, index) in images" :key="index" class="container p-3 my-3 border">
           <h2>{{image.ImageDate}} </h2>
          <img :src ="image.ImageUrl" class="container p-3 my-3" />
            <p></p>
        </div>
        
       

    </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';
import vue from 'vue';
import axios from 'axios';
import moment from 'moment';

export interface Picture {
    NumberInArray: number;
   ImageUrl: string;
   ImageDate: string;
}

export default Vue.extend({
  name: 'HomePage',
  props: {
    msg: String,
    DateToProp: String,
    DateFromProp: String,
  },
  
  created(){
    this.getData()
  },
    data: function () {
        return {
            images: [],
            DateTo: "" ,
            DateFrom:"" 
        }
    },

    methods: {
        getData: function () {
            let dateTo =  moment().format('YYYY/MM/DD');
            let dateFrom = moment().subtract(7, 'd').format('YYYY/MM/DD');

            this.DateTo = dateTo;
            this.DateFrom = dateFrom;

        this.getListOfDates()        
        },
        sortedItems: function() {
          return this.images.sort((a, b) => new Date(b.ImageDate).getDate() - new Date(a
          .ImageDate).getDate()) },




        getListOfDates: function () {
          var dateArray = [];
          for (let index = 1; index < 8; index++) {
            const date = moment().subtract(index, 'd').format('YYYY/MM/DD');
            dateArray.push(date);
                var query = `https://api.nasa.gov/EPIC/api/natural/date/${(moment(date).format('YYYY-MM-DD'))}?api_key=2y37XrAb3R1c7bnBiwIeWjkXwP26QWAdPmNQqRj5`;
                axios.get(query).then(response =>{
                
                  let picture = {} as Picture;
                 
                  picture.ImageUrl =  `https://api.nasa.gov/EPIC/archive/natural/${date}/png/${response.data[7].image}.png?api_key=2y37XrAb3R1c7bnBiwIeWjkXwP26QWAdPmNQqRj5`;
                  picture.ImageDate =  date;
                  picture.NumberInArray = index;

                  this.images.push(picture);
                 
                }).then(()=>{this.sortedItems()})
          }
        }
    },
  
});

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
