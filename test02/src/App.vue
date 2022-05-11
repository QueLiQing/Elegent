<template>
  <div class="max">
    <h1>三生三世</h1>
    <div class="up">
      <span class="btspan">茶颜悦色</span>
      <div class="btb"><b style="color: white">线上点单平台</b></div>
    </div>
    <div class="down">
      <div class="left">
        <span style="width: 150px; font-size: 12px">选择饮品</span
        ><span style="margin-left: 100px; font-size: 12px">规格</span><br />
        <select style="width: 150px" @change="changeteas($event)">
          <option value="红茶">红茶</option>
          <option value="乌龙茶">乌龙茶</option>
          <option value="柠檬茶">柠檬茶</option>
        </select>
        <select style="width: 150px" @change="changetype($event)">
          <option value="中杯">中杯</option>
          <option value="大杯">大杯</option>
          <option value="超大杯">超大杯</option>
        </select>
        <div class="sel">
          <span v-for="item in wd" :key="item"
            ><input
              type="radio"
              name="bing"
              :value="item"
              @click="wdclick(item)"
            />{{ item }}</span
          >
        </div>
        <div class="sel">
          <span v-for="item in tiandu" :key="item"
            ><input
              type="radio"
              name="tian"
              :value="item"
              @click="tianduclick(item)"
            />{{ item }}</span
          >
        </div>
        <div class="sel">
          <span v-for="(item, index) in fl" :key="index">
            <input
              type="checkbox"
              v-model="item.state"
              @click="flclick(item)"
            />{{ item.name }}</span
          >
        </div>
        <button class="xdbtn" @click="xd">下单</button>
      </div>
      <div class="right">
        <table style="text-align: center">
          <tr>
            <th>饮品</th>
            <th>规格</th>
            <th>糖</th>
            <th>温度</th>
            <th>辅料</th>
            <th>操作</th>
          </tr>
          <tr v-for="(item, index) in types" :key="index">
            <td>{{ item.tea }}</td>
            <td>{{ item.type }}</td>
            <td>{{ item.tang }}</td>
            <td>{{ item.wendu }}</td>
            <td style="width: 150px">
              <span v-for="i in item.liao" :key="i">
                <span class="hd" v-if="i=='红豆'">红豆</span>
                <span class="zz" v-if="i=='珍珠'">珍珠</span>
                <span class="ym" v-if="i=='燕麦'">燕麦</span>
                <span class="bd" v-if="i=='布丁'">布丁</span>
              </span>
            </td>
            <!-- style="color: white;border-radius: 5px; margin-left: 2px; " -->
            <td>
              <button
                style="
                  background-color: rgb(12, 135, 243);
                  border: 0;
                  color: white;
                "
                @click="del(index)"
              >
                出货
              </button>
            </td>
          </tr>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      wd: ["常溫", "去冰", "少冰", "去冰"],
      tiandu: ["甜", "七分糖", "半塘", "三分糖", "无糖"],
      fl: [
        {
          name: "红豆",
          state: false,
        },
        {
          name: "珍珠",
          state: false,
        },
        {
          name: "燕麦",
          state: false,
        },
        {
          name: "布丁",
          state: false,
        },
      ],
      types: [
        {
          tea: "紅茶",
          type: "大杯",
          tang: "半塘",
          wendu: "常溫",
          liao: ["红豆", "珍珠"],
        },
        {
          tea: "紅茶",
          type: "大杯",
          tang: "半塘",
          wendu: "常溫",
          liao: ["红豆", "珍珠"],
        },
        {
          tea: "紅茶",
          type: "大杯",
          tang: "半塘",
          wendu: "常溫",
          liao: ["红豆", "珍珠"],
        },
      ],
      tea: "红茶",
      type: "中杯",
      tang: "",
      wendu: "",
      liao: [],
    };
  },
  methods: {
    del(index) {
      this.types.splice(index, 1);
    },
    changeteas(event) {
      this.tea = event.target.value;
      console.log(event.target.value);
    },
    changetype(event) {
      this.type = event.target.value;
      console.log(event.target.value);
    },
    wdclick(value) {
      // this.wendu=i
      console.log(value);
    },
    tianduclick(i) {
      this.tang = i;
    },
    flclick(i) {
      this.liao.push(i.name);
      i.state = true;
    },
    xd() {
      this.types.push({
        tea: this.tea,
        type: this.type,
        tang: this.tang,
        wendu: this.wendu,
        liao: this.liao,
      });
      this.liao = [];
      for (var i = 0; i < this.fl.length; i++) {
        this.fl[i].state = false;
      }
    },
  },
};
</script>

<style>
.hd{
  background-color: red;
  color: aliceblue;
  border-radius: 5px;
  margin-left: 2px;
}
.zz{
  background-color: rgb(62, 187, 245);
  color: aliceblue;
  margin-left: 2px;
  border-radius: 5px;
}
.ym{
  background-color: rgb(255, 196, 0);
  color: aliceblue;
  margin-left: 2px;
  border-radius: 5px;
}
.bd{
  background-color: green;
  color: aliceblue;
  margin-left: 2px;
  border-radius: 5px;
}

.max {
  width: 750px;
  margin: 0 auto;
  padding: 0;
}
.up {
  width: 750px;
  height: 160px;
  padding-top: 30px;
  background-color: rgb(220, 248, 248);
}
.btspan {
  font-size: 50px;
  margin-left: 50px;
}
.btb {
  margin-left: 50px;
  font-size: 12px;
  width: 100px;
  height: 20px;
  line-height: 20px;
  background-color: rgb(29, 245, 21);
  text-align: center;
  border-radius: 10px;
}
.down {
  width: 750px;
  height: 200px;
  margin-top: -20px;
  background-color: rgb(220, 248, 248);
}
.left {
  width: 300px;
  height: 200px;
  float: left;
}
.left .sel {
  height: 40px;
  line-height: 40px;
}
.xdbtn {
  width: 100%;
  height: 30px;
  border: 0;
  background-color: red;
  color: aliceblue;
  line-height: 30px;
  border-radius: 5px;
}
.right {
  width: 450px;
  height: 200px;
  float: left;
}
th,
td {
  width: 60px;
}
</style>
