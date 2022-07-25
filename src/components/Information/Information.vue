<template>
  <div>
    <h5>1.下面那个是建模的软件?</h5>
    <el-radio-group v-model="oneWhat" class="ml-4">
      <el-radio v-for="(w, i) in whatOne" :key="i" :label="w" size="large">{{
        w
      }}</el-radio>
    </el-radio-group>
  </div>
  <div>
    <h5>2.以下那个游戏是3D游戏?</h5>
    <el-radio-group v-model="twoWhat" class="ml-4">
      <el-radio v-for="(w, i) in whatTwo" :key="i" :label="w" size="large">{{
        w
      }}</el-radio>
    </el-radio-group>
  </div>
  <div class="alignment">
    <h5>3.下面那个建模你觉得最难?</h5>
    <el-radio-group v-model="threeWhat" class="ml-4">
      <div class="txt" v-for="(w, i) in whatThree" :key="i">
        <el-radio :label="w" size="large">{{ w }}</el-radio>
        <img :src="require('../../' + images[i])" alt="" srcset="" />
      </div>
    </el-radio-group>

    <!-- <div class="image" v-for="(w, i) in whatThree" :key="i">
        <el-checkbox :label="w" size="large" />
        <img :src="require('../../' + images[i])" alt="" srcset="" />
      </div> -->
  </div>
  <div>
    <h5><span class="coloRed">*</span>4.年龄</h5>
    <el-radio-group v-model="radio2" class="ml-4">
      <el-radio
        v-for="(w, i) in whatFout"
        :key="i"
        :label="i + 1"
        size="large"
        >{{ w }}</el-radio
      >
    </el-radio-group>
  </div>
  <div>
    <h5><span class="coloRed">*</span>5.您的手机号码是?</h5>
    <el-input
      class="w-50 m-2"
      placeholder="请输入手机号码(已做二级加密)"
      @blur="validationPhone"
      v-model="phone"
    />
  </div>
  <br />
  <el-button color="#a4adb3" @click="submit">提交</el-button>
  <div class="studentInformation">
    <p>最新报名学员</p>
    <table>
      <tr>
        <td>xxx</td>
        <td>xxx</td>
        <td>xxx</td>
      </tr>
      <tr>
        <td>xxx</td>
        <td>xxx</td>
        <td>xxx</td>
      </tr>
      <tr>
        <td>xxx</td>
        <td>xxx</td>
        <td>xxx</td>
      </tr>
      <tr>
        <td>xxx</td>
        <td>xxx</td>
        <td>xxx</td>
      </tr>
      <tr>
        <td>xxx</td>
        <td>xxx</td>
        <td>xxx</td>
      </tr>
    </table>
  </div>
</template>

<script>
import { reactive, ref } from "vue";
import axios from "axios";
export default {
  name: "information",
  setup() {
    let oneWhat = ref("");
    let twoWhat = ref("");
    let threeWhat = ref("");
    const problem = reactive({
      whatOne: ["Excel", "3Dsmax", "Photoshop"],
      whatTwo: ["王者荣耀", "英雄联盟", "绝地求生", "以上都是"],
      whatThree: ["任务建模", "道具建模", "场景建模"],
      whatFout: ["17岁以下", "18-20岁", "21-24岁"],
      whatFilter: "",
      images: [
        "assets/选项_人物建模.gif",
        "assets/选项_道具建模.gif",
        "assets/选项_场景建模.gif",
      ],
    });
    let radio2 = ref(0);
    let phone = ref("");
    function submit() {
      if (radio2.value < 1 || radio2.value > 3) {
        alert("年龄为必填项，请选择");
        return;
      }
      if(!validationPhone()) return;
      console.log(oneWhat.value);
      console.log(twoWhat.value);
      console.log(threeWhat.value);
      axios({
        url: "http://124.71.73.195:7766/mt ",
        method: "post",
        headers: { "Content-type": "application/json" },
        params: {
          formStr: `${oneWhat.value},${twoWhat.value},${threeWhat.value}`,
          phone: "13650854572",
          empName: "何天祥",
        },
      }).then(
        (res) => {
          console.log(res.data);
        },
        (rej) => {
          console.log(rej.message);
        }
      );
    }
    function validationPhone() {
      if (
        !/^(13[0-9]|14[579]|15[0-3,5-9]|16[6]|17[0135678]|18[0-9]|19[89])\d{8}$/.test(
          phone.value
        )
      ) {
        alert("手机号格式错误");
        return false
      }
      return true
    }
    return {
      ...problem,
      radio2,
      submit,
      phone,
      validationPhone,
      oneWhat,
      twoWhat,
      threeWhat,
    };
  },
};
</script>

<style lang="less">
.el-checkbox__input.is-checked + .el-checkbox__label {
  color: rgb(164, 166, 170);
}
.el-radio-group {
  width: 46.875rem;
  display: flex;
  flex-direction: row;
  .txt {
    display: flex;
    flex-direction: column;
  margin-right: 20px;
  }
  img {
    width: 200px;
    height: 110px;
  }
}
.coloRed {
  color: red;
}
.el-button {
  width: 700px !important;
  background-color: #a4adb3 !important;
  & > span {
    color: rgb(255, 255, 255);
  }
}
.studentInformation {
  border: 2px solid #cbcbcb;
  margin-top: 30px;
  margin-bottom: 50px;
  text-align: center;
  table {
    width: 500px;
    margin: 0 auto;
  }
}
</style>