<template>
  <div>
    <transition name="sideShow">
      <div class="aside" v-if="open" style="z-index: 99999;" @click="asideClose">
        <div class="aside-content" @click="asideKeep" style="z-index: 100000">
          <div class="col-md-12 d-flex justify-content-end pb-3">
            <a href="#" class="closeAside" @click.prevent="closesidebtn">
              <i class="fas fa-times text-dark"></i>
            </a>
          </div>
          <div class="d-flex justify-content-center member-block pb-3" v-if="login_check == 1">
            <div>
              <MemberAvatar/>
            </div>
            <div class="ml-3">
              <span class="member-name">{{ userinformation.nickname }}</span>
              <p class="member-mail mb-0">{{ userinformation.email }}</p>
              <div>
                <span v-if="userinformation.vip == 1" class="member-level">
                  <img src="../assets/image/icon/ic_vip皇冠.svg" alt=""/>VIP會員
                </span>
                <span class="member-lv">
                  <!-- <img src="../assets/image/badge/Lv20.png"/> -->
                  Lv.{{ userinformation.level }}
                </span>
              </div>
            </div>
          </div>
          <div class="aside-menu">
            <a v-if="login_check == 0" class="text-center">愛台灣<br>和我們一起從溫度開始</a>
            <router-link to="/postdiary" class="btn wanna-post d-flex align-items-center mb-2 sidebtn" v-if="login_check == 1">
              <img
                src="../assets/image/icon/postIcon.svg"
                alt=""
                class="post-img"
              />
              我要發日記
            </router-link>
            <ul class="list-unstyled">
              <!--1220px 後才收進選單start-->
              <div class="d-none apply-aside-menu">
                  <li class="py-2">
                    <router-link to="/harvestSeason" class="d-flex align-items-center">
                      <img src="../assets/image/navbar/ic_harvest_festival.svg" alt="" class="pr-1 cust-aside-img"/>
                      <span>豐收祭</span>
                    </router-link>
                  </li>
                  <li class="py-2">
                    <router-link to="/arena" class="d-flex align-items-center"
                      ><img
                        src="../assets/image/navbar/ic_arena.svg"
                        alt=""
                        class="pr-1 cust-aside-img"
                      /><span>競技場</span>
                      </router-link>
                  </li>
                  <li class="py-2">
                    <router-link to="/missionpage" class="d-flex align-items-center"
                      ><img
                        src="../assets/image/navbar/ic_task.svg"
                        alt=""
                        class="pr-1 cust-aside-img"
                      /><span>任務</span>
                    </router-link>
                  </li>
                  <li class="py-2">
                    <a data-toggle="collapse" aria-expanded="false" aria-controls="huntgroundPage" href="#huntgroundPage" class="d-flex align-items-center"
                      ><img
                        src="../assets/image/navbar/ic_hunt_ground.svg"
                        alt=""
                        class="pr-1 cust-aside-img"
                      /><span>獵場</span>
                    </a>
                    <div class="huntgroundPage-block collapse" id="huntgroundPage">
                      <div class="d-flex flex-column align-items-center">
                        <router-link to="/localhuntground">在地獵場</router-link>
                        <router-link to="/huntground">同好獵場</router-link>
                      </div>
                    </div>
                  </li>
                  <li class="py-2">
                    <router-link to="/notice" class="d-flex align-items-center">
                      <img
                        src="../assets/image/navbar/ic_nonotice.svg"
                        alt=""
                        class="pr-1 cust-aside-img"
                      />
                      <span>通知</span>
                    </router-link>
                  </li>
                  <li class="py-2">
                    <a
                      class="d-flex align-items-center"
                      data-toggle="modal"
                      data-target="#loginModal"
                      style="cursor: pointer;"
                    >
                      <span>登入/註冊</span>
                    </a>
                  </li>
              </div>
              <!--1220px 後才收進選單end-->
              <div v-if="login_check == 1">
                <li class="pb-2">
                  <router-link to="/membercenter" class="d-flex align-items-center">
                    <img src="../assets/image/navbar/mb/ic_person.svg" alt="" class="pr-1">
                      個人主頁
                  </router-link>
                </li>
                <li class="py-2">
                  <router-link to="/memberdiary" class="d-flex align-items-center">
                    <img src="../assets/image/navbar/mb/ic_book.svg" alt="" class="pr-1"/>
                    <span>我的日記</span>
                  </router-link>
                </li>
                <li class="py-2">
                  <router-link to="/ptphuntground" class="d-flex align-items-center">
                    <img src="../assets/image/navbar/mb/ic_fence.svg" alt="" class="pr-1"/>
                    <span>我的獵場</span>
                  </router-link>
                </li>
                <li class="py-2">
                  <router-link to="/giftCab" class="d-flex align-items-center">
                    <img src="../assets/image/navbar/mb/ic_gift.svg" alt="" class="pr-1"/>
                    <span>我的禮物櫃</span>
                  </router-link>
                </li>
                <li class="py-2">
                  <router-link to="/giftshop" class="d-flex align-items-center">
                    <img src="../assets/image/navbar/mb/ic_shop.svg" alt="" class="pr-1" />
                    <span>部落商店</span>
                  </router-link>
                </li>
                <li class="py-2">
                  <router-link to="/tradingRecord" class="d-flex align-items-center">
                    <img src="../assets/image/navbar/mb/ic_list.svg" alt="" class="pr-1"/>
                    <span>交易紀錄</span>
                  </router-link>
                </li>
                <li class="py-2">
                  <router-link to="/myadmgmt" class="d-flex align-items-center">
                    <img src="../assets/image/navbar/mb/ic_AD.svg" alt="" class="pr-1"/>
                    <span>我的廣告</span>
                  </router-link>
                </li>
                <li class="py-2">
                  <router-link to="/myticket" class="d-flex align-items-center">
                    <img src="../assets/image/navbar/mb/ic_ticket.svg" alt="" class="pr-1"/>
                    <span>我的票券</span>
                  </router-link>
                </li>
                <li class="py-2">
                  <router-link to="/favArticles" class="d-flex align-items-center">
                    <img src="../assets/image/navbar/mb/ic_collect.svg" alt="" class="pr-1"/>
                    <span>收藏的文章</span>
                  </router-link>
                </li>
                <li class="py-2">
                  <a class="d-flex align-items-center" data-toggle="collapse" aria-expanded="false" aria-controls="particpage" href="#particpage">
                    <img src="../assets/image/navbar/mb/ic_join.svg" alt="" class="pr-1"/>
                    <span>曾參與的</span>
                    <i class="fas fa-sort-down pb-1 ml-1" style="font-size:18px;"></i>
                  </a>
                  <div class="particpage-block collapse" id="particpage">
                    <div class="d-flex flex-column align-items-center">
                      <router-link to="/participated">抽獎</router-link>
                      <router-link to="/particRace">競賽</router-link>
                      <router-link to="/particMission">任務</router-link>
                    </div>
                  </div>
                </li>
                <li class="py-2">
                  <router-link to="/personalSetting" class="d-flex align-items-center">
                    <img src="../assets/image/navbar/mb/ic_setting.svg" alt="" class="pr-1"/>
                    <span>個人設定</span>
                  </router-link>
                </li>
                <li class="py-2">
                  <router-link to="/" class="d-flex align-items-center">
                    <img src="../assets/image/navbar/mb/ic_signout.svg" alt="" class="pr-1"/>
                    <span>登出</span>
                  </router-link>
                </li>
              </div>
            </ul>
          </div>
        </div>
      </div>
    </transition>
  </div>
</template>
<script>
import MemberAvatar from '../components/MemberAvatar.vue'
export default {
  props: ['open'],
  components: {
    MemberAvatar
  },
  data () {
    return {
    }
  },
  methods: {
    asideClose () {
      this.$emit('prevClick', false)
    },
    asideKeep (e) {
      this.$emit('keepshow', true)
      e.stopPropagation() // 點擊子元件不影響父層元件
    },
    closesidebtn (e) {
      this.$emit('togglenav', false)
      e.stopPropagation() // 點擊子元件不影響父層元件
    }
  },
  computed: {
    userinformation () {
      const userInf = JSON.parse(this.$store.state.user)
      return userInf
    },
    login_check () {
      return this.$store.state.login_status
    }
  }
}
</script>
<style lang="scss" scoped>
.fadetable {
  left: 0;
  background: rgba($color: #000000, $alpha: 1.0);
}
  .sideShow {
    &-enter, &-leave-to {
      opacity: 0;
      transform: translateX(100%);
    }
    &-enter-active, &-leave-active {
      transition: all 500ms;
    }
  }
  .huntgroundPage-block {
    div {
      width: 50%;
    }
  }
</style>
