<!-- 通用手机预览组件 - by ZHJ - ver: 20190618 -->
<!--
props:
type: 预览类型 (type: String, 取值为 'iframe'，'content')
url: 需要预览的页面的url（type: String）
content: 需要预览的内容的HTML代码（type: String）
showTopBar: 是否显示顶部导航栏（type: Boolean）
-->

<template lang="html">
  <div class="mobile_preview_component">
    <div class="mobile_preview_top_bar clearfix" v-if="showTopBar">
      <div class="mobile_preview_top_bar_back left" @click="goBack">返回</div>
      <div class="mobile_preview_top_bar_dots right">
        <span></span>
        <span></span>
        <span></span>
      </div>
    </div>
    <iframe class="mobile_preview_iframe" :class="{'no_top_bar': !showTopBar}" :src="url" width="360" height="610" v-if="type === 'iframe'"></iframe>
    <div class="mobile_preview_content" :class="{'no_top_bar': !showTopBar}" v-html="content" v-if="type === 'content'"></div>
  </div>
</template>

<script>
  export default {
    props: {
      type: {
        type: String
      },
      url: {
        type: String
      },
      content: {
        type: String
      },
      showTopBar: {
        type: Boolean
      }
    },
    methods: {
      goBack() {
        window.history.back();
      },
    },
  }
</script>

<style lang="scss" scoped>

  // 通用样式
  .clearfix:before, .clearfix:after {
    content: "";
    display: table;
  }
  .clearfix:after {
    clear: both;
  }
  .clearfix {
    *zoom: 1;/*IE/7/6*/
  }

  .left {
    float: left;
  }
  .right {
    float: right;
  }

  // 组件样式
  .mobile_preview_component {
    box-sizing: border-box;
    width: 380px;
    margin: 5px auto;
    height: 750px;
    background-color: #000;
    border-radius: 30px;
    padding: 50px 10px;
    position: relative;
    &:before {
      content: "";
      display: block;
      box-sizing: border-box;
      width: 60px;
      height: 6px;
      background-color: #555;
      position: absolute;
      top: 22px;
      left: 160px;
      border-radius: 5px;
    }
    &:after {
      display: block;
      box-sizing: border-box;
      content: "";
      width: 36px;
      height: 36px;
      border-radius: 50%;
      position: absolute;
      bottom: 7px;
      left: 172px;
      border: 5px solid #555;
    }

    * {
      box-sizing: border-box;
    }

    .mobile_preview_top_bar {
      width: 100%;
      height: 40px;
      line-height: 40px;
      background-color: #1c1b1b;
      .mobile_preview_top_bar_back {
        color: #aaa;
        font-size: 16px;
        font-weight: bold;
        padding: 0 30px;
        cursor: pointer;
        position: relative;
        &:before {
          content: "";
          position: absolute;
          width: 10px;
          height: 10px;
          border: 1px solid #aaa;
          border-width: 2px 0 0 2px;
          transform: rotate(315deg);
          top: 14px;
          left: 15px;
        }
      }
    }

    .mobile_preview_top_bar_dots {
      padding-right: 10px;
      span {
        display: inline-block;
        width: 5px;
        height: 5px;
        border-radius: 50%;
        background-color: #aaa;
        & + span {
          margin-left: 2px;
        }
      }
    }

    .mobile_preview_iframe, .mobile_preview_content {
      display: block;
      border: none;
      background-color: #fff;
      height: 610px;
    }

    .mobile_preview_iframe {
      &.no_top_bar {
        height: 650px !important;
      }
    }

  }

</style>

<style lang="scss">

  .mobile_preview_component {
    .mobile_preview_content {
      line-height: normal;
      overflow-y: scroll;
      &.no_top_bar {
        height: 650px !important;
      }
      img {
        max-width: 100%;
        height: auto;
      }
      video {
        max-width: 100%;
        max-height: 200px;
      }
      audio {
        max-width: 100%;
        max-height: 80px;
      }
    }

  }
</style>
