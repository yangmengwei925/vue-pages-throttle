<template>
  <div class="hello">
    <div class="form-wrap">
      <div class="form-group"><span class="form-label">姓名</span><input type="text" v-model="fullname"></div>
      <div class="form-group"><span class="form-label">性别</span><input id="radio1" type="radio" v-model="sex" value="男"><label for="radio1">男</label><input id="radio2" type="radio" v-model="sex" value="女"><label for="radio2">女</label></div>
      <div class="form-ft">
        <button @click="Submit">提交</button>
      </div>
    </div>
    <div class="form-res">
      <h5>提交后：</h5>
      <p>提交次数：{{formData.count}}</p>
      <p>姓名：{{formData.fullname}}</p>
      <p>性别：{{formData.sex}}</p>
    </div>
  </div>
</template>

<script>
import { Debounce } from '../utils/pubulic'

export default {
  name: 'Home',
  data () {
    return {
      fullname: '',
      sex: '',
      formData: {
        fullname: '',
        sex: '',
        count: 0
      }
    }
  },
  methods: {
    Submit: Debounce(function () {
      this.formData.fullname = this.fullname;
      this.formData.sex = this.sex;
      this.formData.count++
    }, 3000)
  }
}
</script>

<style scoped>
.form-wrap {
  margin: 30px;
  border: 1px solid #eee;
  border-radius: 3px;
  width: 300px;
  padding: 15px;
}
  .form-group {
    display: flex;
    margin-bottom: 10px;
  }
    .form-label {
      margin-right: 10px;
    }
  
  .form-ft {
    text-align: center;
    margin-top: 20px;
  }

.form-res {
  margin: 0 30px;
  padding: 15px;
}
  h5 {
    margin-bottom: 10px;
  }
  p {
    margin-bottom: 5px;}

</style>