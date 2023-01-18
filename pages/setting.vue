<template>

  <v-container>
    <div class="wrapper_page">
      <h1 class="mb-10">ข้อมูลการตั้งค่า</h1>

      <div
        v-for="item, i in items"
        :key="i"
        class="warpper-input card mt-2"
      >
        <v-col cols="8" style="text-align: left; line-height: 35px">
             
          <h1> {{ item.time_start }} </h1>
          <h1> {{ item.time_end }} </h1>
          <p> การเปิด : {{ item.day }} </p>

        </v-col>


        <v-col cols="2">
          <v-switch color="success" v-model="item.status" inset></v-switch>
        </v-col>

        <v-col cols="2">
          <v-btn icon color="red">
            <v-icon size="40">mdi-trash-can</v-icon>
          </v-btn>
        </v-col>

      </div>
      <v-btn
        block
        elevation="2"
        class="my-10"
        color="#526FFF"
        style="color: #fff; border-radius: 15px"
        to="/setting_templatetime"
        ><v-icon size="20">mdi-plus</v-icon>เพิ่ม</v-btn
      >
    </div>
  </v-container>
</template>

<script>

import axios from 'axios';

let t_start = [];
let t_end = [];
let s_day = [];
let id = [];
var counter = 5;
axios.get('http://127.0.0.1:4003/chk_count').then((response) => {

  // counter = response.data.count
  // counter = 5 
  console.log(response.data.count)  

  axios.get('http://127.0.0.1:4003/getdata_day').then((response) => {
    for(var i=0 ; i<counter; i++){
      t_start[i] = response.data[i].H_on + ":" + response.data[i].M_on
      t_end[i] = response.data[i].H_off + ":" + response.data[i].M_off
      s_day[i] = response.data[i].daystart
      id[i] = response.data[i].id

      console.log(id[i])
      console.log(t_start[i])
      console.log(t_end[i])
      console.log(s_day[i])
    }
    console.log(response.data)
          // t_start = response.data[i].H_on + ":" + response.data[i].M_on
          // t_end = response.data[i].H_off + ":" + response.data[i].M_off
          // s_day = response.data[i].daystart
          
              
    });
});





export default {
  data() {

    return {
      count: counter,
      status: true,
      items: [
        {
          id: 1,
          time_start: t_start[0],
          time_end: t_end[0],
          day: s_day[0],
          status: true,

          // id: 1,
          // time_start: t_start,
          // time_end: t_end,
          // day: s_day,
          // status: true,

        },
        {
          id: 2,
          time_start: t_start[1],
          time_end: t_end[1],
          day: s_day[1],
          status: true,
        },
        {
          id: 3,
          time_start: t_start[2],
          time_end: t_end[2],
          day: s_day[2],
          status: true,
        },
        {
          id: 4,
          time_start: t_start[3],
          time_end: t_end[3],
          day: s_day[3],
          status: true,
        },
        {
          id: 5,
          time_start: t_start[4],
          time_end: t_end[4],
          day: s_day[4],
          status: true,
        }
      ],
    };
  },
};

</script>


<style lang="scss" scoped>
.wrapper_page {
  align-content: center;
  p {
    margin: 0px;
  }
  .warpper-input {
    display: flex;
    flex-direction: row;
    padding: 10px;
    align-items: center;
    border-bottom: 1px solid #c4c4c4;
  }
}
</style>