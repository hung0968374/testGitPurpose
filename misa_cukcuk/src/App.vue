<template>
  <div id="app1" v-bind:class="{handleDialog: showDialog }">
      <Menu />
      <Header />
      <Content :listDatas = "content" 
      v-on:openDialog = 'changingDiaStt'
      v-on:emitCusInfo = 'changingDiaStt_actDelBttn_emitEmId'
      v-on:sortByCate = 'sortEmByCategory'
      v-on:sortByPos = 'sortEmByPosition' />
      <Dialog :cusInfo="cusInfo" v-if="showDialog"
      v-on:dialogStatusChanged = "changingDiaStt"
      :affectedByDiaStt = "affectedByDiaStt"
      :selectedEm = "this.cusInfo"
      :showEditEmInfoDia = "showEditEmInfoDia"/>
  </div>
</template>

<script>
import Menu from './components/menu';
import Header from './components/header';
import Content from './components/content';
import Dialog from './components/dialog';
import axios from 'axios';
//import VueFilterDateFormat  from 'vue-filter-date-format';

export default {
  name: 'App',
  components: {
    Menu,
    Header,
    Content,
    Dialog
  },
  data() {
    return {
      content : [
      ],
      cusInfo:[
        {
          BaseSalary:"", 
          Category:"", 
          DateJoinFirm:"", 
          DateOfBirth:"", 
          Email:"", 
          EmployeeCode:"", 
          EmployeeId:"", 
          FullName:"", 
          Gender:"", 
          GivenDate:"", 
          GivenPlace:"", 
          IdentityCard:"", 
          PersonalTax:"", 
          PhoneNumber:"", 
          Position:"", 
          WorkStatus:"", 
        },
      ],
      showDialog: false,
      affectedByDiaStt: true,
      showEditEmInfoDia: false,
    }
  },
  methods: {
    changingDiaStt: function(){
      this.showDialog = !this.showDialog,
      this.affectedByDiaStt = true;
      this.showEditEmInfoDia = false;
    },
     changingDiaStt_actDelBttn_emitEmId(employeeId){
        this.affectedByDiaStt = true;
        this.showDialog = !this.showDialog;
        this.affectedByDiaStt = !this.affectedByDiaStt;
        this.cusInfo = employeeId;
        this.showEditEmInfoDia = true;
    },
    async sortEmByCategory(url){
      const res = await axios.get('http://localhost:52319/api/Employees/search?sortByName='+url)
      console.log(res.data);
      this.content = res.data;
    },
    async sortEmByPosition(url){
      const res = await axios.get('http://localhost:52319/api/Employees/search?sortByName='+url)
      console.log(res.data);
      this.content = res.data;
    },
  },
  async created (){
    const response = await axios.get('http://localhost:52319/api/Employees')
    this.content = response.data;
  }
}
</script>

<style>
  * {
    margin: 0px;
  }
  #app1 {
    margin: 0px;
    height: 98vh;
  }
  .handleDialog {
    background-color: #69696954;
  }
</style>
