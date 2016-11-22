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
    <transition name="fade">
      <div class="detail" v-show="detailShow">
        <div class="detail-wrapper clearfix">
          <div class="detail-main">
            <h1 class="name">{{ seller.name }}</h1>
            <div class="star-wrapper">
              <star :size="48" :score="seller.score"></star>
            </div>
            <div class="title">
              <div class="line"></div>
              <div class="text">优惠信息</div>
              <div class="line"></div>
            </div>
            <ul v-if="seller.supports" class="supports">
              <li class="support-item" v-for="item in seller.supports">
                <span class="icon" :class="classMap[item.type]"></span>
                <span class="text">{{ item.description }}</span>
              </li>
            </ul>
            <div class="title">
              <div class="line"></div>
              <div class="text">商家公告</div>
              <div class="line"></div>
            </div>
            <div class="bulletin">
              <p class="content">{{ seller.bulletin }}</p>
            </div>
          </div>
        </div>
        <div class="detail-close" @click="showDetail">
          <i class="sell-icon icon-cuowu"></i>
        </div>
      </div>
    </transition>
  </div>
</template>

<script type="text/ecmascript-6">
  import star from 'components/star/star';

  export default{
    props: {
      seller: {
        type: Object
      }
    },
    created() {
      this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee'];
    },
    components: {
      star
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
      background: rgba(7, 17, 27, 0.8);
      backdrop-filter: blur(10px);
      &.fade-enter-active {
        transition: all .3s;
      }
      &.fade-enter, &.fade-leave-active {
        transition: all .3s;
        padding-top: 100px;
        opacity: 0;
        background: rgba(7, 17, 27, 0);
      }
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
          .star-wrapper {
            margin-top: 18px;
            padding: 2px 0;
            text-align: center;
          }
          .title {
            display: flex;
            width: 80%;
            margin: 28px auto 24px auto;
            .line {
              flex: 1;
              position: relative;
              top: -6px;
              border-bottom: 1px solid rgba(255, 255, 255, 0.2);
            }
            .text {
              padding: 0 12px;
              font-weight: 700;
              font-size: 14px;
            }
          }
          .supports {
            width: 80%;
            margin: 0 auto;
            .support-item {
              padding: 0 12px;
              margin-bottom: 12px;
              font-size: 0;
              &:last-child {
                margin-bottom: 0;
              }
              .icon {
                display: inline-block;
                width: 16px;
                height: 16px;
                vertical-align: top;
                margin-right: 6px;
                background-size: 16px 16px;
                background-repeat: no-repeat;
                &.decrease {
                  @include bg-img('decrease_2');
                }
                &.discount {
                  @include bg-img('discount_2');
                }
                &.guarantee {
                  @include bg-img('guarantee_2');
                }
                &.invoice {
                  @include bg-img('invoice_2');
                }
                &.special {
                  @include bg-img('special_2');
                }
              }
              .text {
                line-height: 16px;
                font-size: 12px;
              }

            }
          }
          .bulletin {
            width: 80%;
            margin: 0 auto;
            .content {
              padding: 0 12px;
              line-height: 24px;
              font-size: 12px;
            }
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
