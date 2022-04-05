<template>
  <img alt="Vue logo" src="../assets/logo.png" />
  <button type="button" class="btn btn-primary" v-on:click="compare()">
    比較
  </button>
  <button type="button" class="btn btn-danger" v-on:click="clearDatas()">
    清空
  </button>
  <div class="home">
    <div class="row">
      <div class="col-6">
        <div>帳單</div>
        <form>
          <input type="number" v-model="curBillNum" id="billInput" />
          <button type="button" v-on:click="clickBill()">加入清單</button>
        </form>

        <div v-for="(data, index) in billArray" :key="index">
          {{ data }}
        </div>
      </div>
      <div class="col-6">
        <div>消費紀錄</div>
        <form>
          <input type="number" v-model="curRecordNum" id="RecordInput" />
          <button type="button" v-on:click="clickRecord()">加入清單</button>
        </form>

        <div v-for="(data, index) in recordArray" :key="index">
          {{ data }}
        </div>
      </div>
    </div>

    <!-- <HelloWorld msg="Welcome to Your Vue.js + TypeScript App" /> -->
  </div>
</template>

<script lang="ts">
import { Options, Vue } from "vue-class-component";
import HelloWorld from "@/components/HelloWorld.vue"; // @ is an alias to /src

@Options({
  components: {
    HelloWorld,
  },
})
export default class HomeView extends Vue {
  curBillNum = 0;
  billArray: Array<number> = [];

  curRecordNum = 0;
  recordArray: Array<number> = [];

  testFunc() {
    let aaa = "rqr";
    console.log(aaa);
  }

  clickBill() {
    let addData = this.curBillNum;
    this.billArray.push(addData);
    this.curBillNum = 0;
  }

  clickRecord() {
    let addData = this.curRecordNum;
    this.recordArray.push(addData);
    this.curRecordNum = 0;
  }

  compare() {
    let alertContent = "";
    let billWrongArray: Array<number> = [];
    // let recordWrongArray: Array<number> = [];
    let newAry = this.recordArray.map((n) => n);
    for (let i = 0; i < this.billArray.length; i++) {
      const checkNum = this.billArray[i];
      const index = newAry.indexOf(checkNum);
      if (index != -1) {
        newAry.splice(index, 1);
      } else {
        billWrongArray.push(checkNum);
      }
    }

    if (billWrongArray.length > 0) {
      alertContent =
        alertContent + "帳單多出" + billWrongArray.join(",") + "\n";
    }

    if (newAry.length > 0) {
      alertContent = alertContent + "消費紀錄多出" + newAry.join(",");
    }

    if (alertContent.length > 0) {
      alert(alertContent);
    } else {
      alert("相同");
    }
  }

  clearDatas() {
    this.curBillNum = 0;
    this.billArray = [];
    this.curRecordNum = 0;
    this.recordArray = [];
  }
}
</script>
