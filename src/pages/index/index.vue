<template>
  <div class="index">
    <!-- <div class="radio1">
      <h1>缩放动画</h1>
      <div v-for="(item,index) in dateInfo" :key="index" @click="clickHandle(index)">
        <input type="radio" name="ys" :id="item.value" />
        <label :for="item.value" :class="{'checked':item.checked}"></label>
        <p>{{item.meaning}}</p>
      </div>

    </div> -->
    <div class="radio2">
      <h1>旋转动画</h1>
      <div v-for="(item,index) in dateInfo" :key="index" @click="clickHandle(index)">
        <input type="radio" name="ys" :id="item.value" />
        <label :for="item.value" :class="{'checked':item.checked}"></label>
        <p>{{item.meaning}}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      motto: 'Hello miniprograme',
      userInfo: {
        nickName: 'mpvue',
        avatarUrl: 'http://mpvue.com/assets/logo.png'
      },
      dateInfo: [
        {
          meaning: '8月1日',
          value: '0801',
          checked: false
        },
        {
          meaning: '8月14日',
          value: '0814',
          checked: false
        },
        {
          meaning: '8月28日',
          value: '0828',
          checked: false
        }
      ],
      className: 'posfirst'
    }
  },

  mounted () {
  },
  methods: {
    bindViewTap () {
      const url = '../logs/main'
      if (mpvuePlatform === 'wx') {
        mpvue.switchTab({ url })
      } else {
        mpvue.navigateTo({ url })
      }
    },
    clickHandle (index) {
      this.dateInfo.forEach(element => {
        element.checked = false
      })
      this.dateInfo[index].checked = true
    }
  },

  created () {
    // let app = getApp()
  }
}
</script>

<style scoped>
.index {
  width: 100%;
  height: 750px;
  background: #708fd4;
}

 body {
  background-color: #EEEEEE;
}
h1{
    color: #DC143C;
}
.radio1,.radio2{
    /* border: 1px solid #DC143C; */
    border-radius: 12px;
    margin-top: 10px;
    padding: 10px;
    display: flex;
    flex-direction: column
}
.radio1 div,.radio2 div{
  display: flex;
  margin-top: 20px
}
.radio1 div p,.radio2 div p{
  margin: auto 0;
  font-size: 20px;
  margin-left: 20px;
  color: #fff
}
.radio1 label {
    display: inline-block;
    position: relative;
    width: 28px;
    height: 28px;
    border: 1px solid #ccc;
    background-color: #FFF;
    cursor: pointer;
    border-radius: 50%;
    /* margin-top: 20px; */
}
/*核心就是把label变成了单选框的样式，把radio隐藏起来，因为选中label就会选中对应的额radio，所以用户不必直接选radio了，而是通过label变相的来选中radio。但好处就是label可以加动画样式。*/
/*给label的后边加一个动画*/

.radio1 label:after {
    content: "";
    position: absolute;
    top: 4px;
    left: 4px;
    width: 20px;
    height: 20px;
    border-radius: 50%;
    background-color: #1F8CEB;
    -moz-transform: scale(0);
    -webkit-transform: scale(0);
    -ms-transform: scale(0);
    -o-transform: scale(0);
    transform: scale(0);
    -moz-transition: transform .5s ease-out;
    -webkit-transition: transform .5s ease-out;
    -o-transition: transform .5s ease-out;
    -ms-transition: transform .5s ease-out;
    transition: transform .5s ease-out;
}
/*把小黑点做出来，缩放为0.做出来的方法，是在label的后边加上了一个空伪类，然后填充颜色*/

.radio1 .checked {
    /*这既是灵活运用伪类选择器和兄弟选择器了。checked表示被选中的那个radio，+表示那个radio下边的近邻label*/
    background-color: #eee;
    -moz-transition: transform .2s ease-out;
    -webkit-transition: transform .2s ease-out;
    -ms-transition: transform .2s ease-out;
    -o-transition: transform .2s ease-out;
    transition: transform .2s ease-out;
}

.radio1 .checked+p{
  color: #1F8CEB
}

.radio1 .checked:after {
    -moz-transform: scale(1);
    -ms-transform: scale(1);
    -webkit-transform: scale(1);
    -o-transform: scale(1);
    transform: scale(1);
    -moz-transition: transform .5s ease-out;
    -webkit-transition: transform .5s ease-out;
    -o-transition: transform .5s ease-out;
    -ms-transition: transform .5s ease-out;
    transition: transform .5s ease-out;
}

.radio1 input {
    display: none;
}
/*radio2自己练习旋转动画*/
.radio2 label{
    width: 30px;
    height: 30px;
    background-color: coral;
    display: inline-block;
    border-radius: 50%;
    border: 1px solid #D2B48C;
    margin-right: 5px;
    position: relative;
    cursor: pointer;
    overflow: hidden;
}
.radio2 label:after{
    content: "";
    width: 20px;
    height: 20px;
    background-color: #90EE90;
    position: absolute;
    top: 5px;
    left: 5px;
    border-radius: 50%;
    transform: rotate(-180deg);
    transform-origin: -3px 50%;
    transition: transform .7s ease-out;
}
.radio2 .checked{
    background-color: #4169E1;
    transition: background-color .7s ease-out;
}

.radio2 .checked+p{
  color: #90EE90
}

.radio2 .checked:after{
    transform: rotate(0deg);
    transition: transform .7s ease-out;
}
.radio2 input{
    display: none;
}
</style>
