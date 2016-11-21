<template>
  <div class="header">
    <div class="content-wrapper">
      <div class="avatar">
        <img width="64" height="64" :src="seller.avatar" alt="">
      </div>
      <div class="content">
        <div class="title">
          <span class="brand"></span>
          <span class="name">{{ seller.name }}</span>
        </div>
        <div class="desc">
          {{ seller.description }} / {{ seller.deliveryTime }}分钟送达
        </div>
        <div v-if="seller.supports" class="supports">
          <span class="icon" :class="this.classMap[seller.supports[0].type]"></span>
          <span class="text">{{ seller.supports[0].description }}</span>
        </div>
      </div>
      <div class="supports-count" v-if="seller.supports" @click="showDetail">
        <span class="count">{{ seller.supports.length }}个</span>
        <i class="sell-icon icon-youjiantou-01"></i>
      </div>
    </div>
    <div class="bulletin-wrapper" @click="showDetail">
      <span class="bulletin-title"></span>
      <span class="bulletin-text">{{ seller.bulletin }}</span>
      <i class="sell-icon icon-youjiantou-01"></i>
    </div>
    <div class="background">
      <img :src="seller.avatar" width="100%">
    </div>
    <div class="detail" v-show="detailShow">
      <div class="detail-wrapper clearfix">
        <div class="detail-main">
          <h1 class="name">{{ seller.name }}</h1>
        </div>
      </div>
      <div class="detail-close" @click="showDetail">
        <i class="sell-icon icon-cuowu"></i>
      </div>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
  import '../../common/style/icon.scss';
  export default{
    props: {
      seller: {
        type: Object
      }
    },
    created() {
      this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee'];
    },
    data() {
      return {
        detailShow: false
      };
    },
    methods: {
      showDetail() {
        this.detailShow = !this.detailShow;
      }
    }
  };
</script>

<style lang="scss" rel="stylesheet/scss">
  @import "../../common/style/mixin";

  .header {
    position: relative;
    background: rgba(7, 17, 25, 0.5);
    color: #fff;
    .content-wrapper {
      position: relative;
      padding: 24px 12px 18px 24px;
      font-size: 0;
      .avatar {
        display: inline-block;
        vertical-align: top;
        & > img {
          border-radius: 2px;
        }
      }
      .content {
        display: inline-block;
        margin-left: 16px;
        .title {
          margin: 2px 0 8px 0;
          .brand {
            display: inline-block;
            vertical-align: top;
            width: 30px;
            height: 18px;
            @include bg-img('brand');
            background-size: 30px 18px;
            background-repeat: no-repeat;
          }
          .name {
            margin-left: 6px;
            font-size: 16px;
            line-height: 18px;
            font-weight: bold;
          }
        }
        .desc {
          margin-bottom: 10px;
          line-height: 12px;
          font-size: 12px;
        }
        .supports {
          font-size: 12px;
          .icon {
            display: inline-block;
            vertical-align: top;
            width: 12px;
            height: 12px;
            margin-right: 4px;
            background-size: 12px;
            background-repeat: no-repeat;
            &.decrease {
              @include bg-img('decrease_1');
            }
            &.discount {
              @include bg-img('discount_1');
            }
            &.guarantee {
              @include bg-img('guarantee_1');
            }
            &.invoice {
              @include bg-img('invoice_1');
            }
            &.special {
              @include bg-img('special_1');
            }
          }
          .text {
            font-size: 10px;
          }
        }
      }
      .supports-count {
        position: absolute;
        right: 12px;
        bottom: 18px;
        padding: 0 8px;
        height: 22px;
        line-height: 22px;
        border-radius: 14px;
        font-size: 12px;
        background: rgba(0, 0, 0, 0.2);
        text-align: center;
        .count {
          vertical-align: top;
          font-size: 10px;
        }
        .icon-youjiantou-01 {
          margin-left: 0px;
          font-size: 10px;
        }
      }
    }
    .bulletin-wrapper {
      position: relative;
      height: 28px;
      line-height: 28px;
      padding: 0px 22px 0 12px;
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
      background-color: rgba(27, 27, 27, 0.2);
      .bulletin-title {
        display: inline-block;
        vertical-align: top;
        margin-top: 8px;
        width: 22px;
        height: 12px;
        @include bg-img('bulletin');
        background-size: 22px 12px;
        background-repeat: no-repeat;
      }
      .bulletin-text {
        vertical-align: top;
        font-size: 10px;
        font-weight: 200;
      }
      .icon-youjiantou-01 {
        position: absolute;
        font-size: 10px;
        right: 12px;
        top: 8px;
      }
    }
    .background {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      z-index: -1;
      overflow: hidden;
      filter: blur(10px);
    }
    .detail {
      position: fixed;
      top: 0;
      left: 0;
      z-index: 100;
      width: 100%;
      height: 100%;
      overflow: auto;
      background-color: rgba(7, 17, 27, 0.8);
      .detail-wrapper {
        min-height: 100%;
        width: 100%;
        .detail-main {
          margin-top: 64px;
          padding-bottom: 64px;
          .name {
            text-align: center;
            font-size: 16px;
            font-weight: 700;
          }
        }
      }
      .detail-close {
        position: relative;
        width: 32px;
        height: 32px;
        margin: -64px auto 0 auto;
        clear: both;
        font-size: 32px;
      }
    }
  }
</style>
