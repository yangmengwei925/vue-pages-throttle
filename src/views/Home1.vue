<template>
  <div class="home">
    <!-- <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/> -->
     <div class="mainBlock">
          <!--显示的窗口-->
          <div class="displayWindow">
            <!--可移动面板-->
            <div class="mobilePanel" style="position: relative;left: 0;">
              <div class="box" v-bind:key="index" v-for="(item, index) in productList">
                <div class="boxLeft">
                  <div style="width: 100%;height: 100%;display: flex;justify-content: center">
                    <img :src="item.picSrc" :width="item.picWidth" height="80px" style="margin-top: 14px"/>
                  </div>
                </div>
                <div class="boxRight">
                  <p class="proTitle">{{item.ProductName}}</p>
                  <p class="proText">{{item.Description}}</p>
                </div>
              </div>
            </div>
          </div>
        </div>
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'

// export default {
//   name: 'Home',
//   components: {
//     HelloWorld
//   }
// }
export default {
  name: 'Home',
  data () {
    return {
      productList: [
        {
          ProductName: 'ET-NBAC-I',
          Description: 'ET-NBAC-I三相不平衡智能调控系统是一种智能实时调控装置，...',
          // picSrc: require(),
          picWidth: '80px'
        },
        {
          ProductName: 'ET-NBAC-II',
          Description: 'ET-NBAC-II三相不平衡智能调控系统是一种智能实时调控装置...',
          // picSrc: require(),
          picWidth: '80px'
        },
        {
          ProductName: 'ET-TSC++',
          Description: 'ET-TSC++超快速电容器综合模块，具有速度快、容量大、寿命长...',
          // picSrc: require(),
          picWidth: '80px'
        },
        {
          ProductName: 'ET-D(S)VS',
          Description: '末端电压稳定装置是一种跟踪末端线路电压变化、自...',
          // picSrc: require(),
          picWidth: '80px'
        },
        {
          ProductName: '在线监测系统',
          Description: '电能质量在线监测系统是面向对象的大型电能质量在线监测与管理系统。...',
          picSrc: require(),
          picWidth: '80px'
        },
        {
          ProductName: 'PQ2000',
          Description: 'PQ2000电能质量分析仪是北斗易通结合我国电力系统的特点，采用...',
          // picSrc: require(),
          picWidth: '80px'
        },
        {
          ProductName: 'PQME2000系列',
          Description: 'PQME2000系列是北斗易通公司严格按照国家颁布的相关技术标准...',
          // picSrc: require(),
          picWidth: '80px'
        }
      ]
    }
  },
  mounted () {
    let len = this.productList.length % 4
    // 根据产品数组长度除以4的余数，来给数组末尾加入几个空的object
    switch (len) {
      case 0:
        break
      case 1:
        for (let i = 0; i < 3; i++) {
          this.productList.push(
            {
              ProductName: '',
              Description: '',
              picSrc: '',
              picWidth: '0'
            }
          )
        }
        break
      case 2:
        for (let i = 0; i < 2; i++) {
          this.productList.push(
            {
              ProductName: '',
              Description: '',
              picSrc: '',
              picWidth: '0'
            }
          )
        }
        break
      case 3:
        this.productList.push(
          {
            ProductName: '',
            Description: '',
            picSrc: '',
            picWidth: '0'
          }
        )
        break
      default:
        break
    }
    // 取数组前4个元素，加入到数组末尾去，便于轮播
    let productListFrontFourthObject = this.productList.slice(0, 4)
    for (let i = 0; i < productListFrontFourthObject.length; i++) {
      this.productList.push(productListFrontFourthObject[i])
    }
    // 设置定时，开始轮播
    let _this = this
    setTimeout(function () {
      _this.changeLeftVal()
    }, 3000)
  },
  methods: {
    // 移动面板mobilePanel left属性变化函数
    changeLeftVal () {
      // 变化前移动面板的left属性值
      let beforeLeftVal = parseInt(document.querySelector('.mobilePanel').style.left)
      // 变化后移动面板的left属性值
      let afterLeftVal = beforeLeftVal - 1080
      // 给左移添加动画
      this.animate(beforeLeftVal, afterLeftVal)
    },
    // 动画效果
    animate (beforeLeftVal, afterLeftVal) {
      let _this = this
      var interval
      // 设置定时器，这里设置10ms移动108px，即100ms移动1080px，也就是说动画效果时间为100ms
      interval = setInterval(function () {
        beforeLeftVal -= 108 // left值减108
        document.querySelector('.mobilePanel').style.left = beforeLeftVal + 'px' // 渲染到DOM中
        // 如果beforeLeftVal值已经变化到 等于我们需要的值时
        if (beforeLeftVal === afterLeftVal) {
          // 清初定时器
          clearInterval(interval)
          // 当beforeLeftVal值等于 -1080 × （产品数组长度/4 - 1），将移动面板的left值归零
          if (beforeLeftVal === -1080 * (_this.productList.length / 4 - 1)) {
            document.querySelector('.mobilePanel').style.left = 0
          }
          // 继续改变移动面板left值
          setTimeout(function () {
            _this.changeLeftVal()
          }, 3000)
        }
      }, 10)
    }
  }
}

</script>
<style scoped>
  
.mainBlock {
    width: 1080px;
    margin: 0 auto;
    padding: 20px 0;
    height: 150px;
  }
  .displayWindow {
    width: 100%;height: 100%;overflow: hidden
  }
  .mobilePanel {
    width: 3240px;height: 100%;
  }
  /* .box {
    float: left;width: 270px;height: 120px;background: url(../assets/images/item_bg.jpg) no-repeat center bottom;
  } */
  .boxLeft {
    width: 115px;float: left;height: 100%;
  }
  .boxRight {
    width: 135px;float: left;
  }
  .proTitle {
    line-height: 30px;font-size: 14px;margin: 2px auto;
  }
  .proText {
    color: #666;line-height: 180%;font-size: 12px;margin: 2px auto;
  }

</style>