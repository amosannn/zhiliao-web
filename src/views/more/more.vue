<template>
  <div>
    <!--<mu-appbar class="title"  title="知了">-->
      <!--<mu-flat-button color="white" label="搜索" labelClass="appbar-search-block" icon="search" slot="right"/>-->
      <!--<span class="appbar-text" slot="center">知了</span>-->
      <!--<mu-flat-button color="white" label="提问" labelClass="appbar-search-block" icon="control_point" slot="left"/>-->
      <!--&lt;!&ndash;icon-loupe&ndash;&gt;-->
    <!--</mu-appbar>-->
    <zhiliao></zhiliao>
    <section class="more-lists">
      <mu-list-item :title="user.username" describeText="查看或编辑个人主页" @click="jumpToProfile">
        <mu-avatar :src="user.avatarUrl" slot="leftAvatar"/>
        <!--<span slot="describe">-->
        <!--查看或编辑个人主页-->
        <!--</span>-->
      </mu-list-item>
      <mu-divider inset/>

      <mu-list class="more-lists-content">
        <mu-list-item title="我的创作">
          <mu-icon slot="left" value="create"/>
        </mu-list-item>
        <mu-divider inset/>
        <mu-list-item title="我的关注">
          <mu-icon slot="left" value="remove_red_eye"/>
        </mu-list-item>
        <mu-divider inset/>
        <mu-list-item title="我的收藏" @click.native="jumpToCollection()">
          <mu-icon slot="left" value="star"/>
        </mu-list-item>
        <mu-divider/>
      </mu-list>


      <mu-list class="more-lists-content">
        <mu-sub-header>账号设置</mu-sub-header>
        <mu-list-item title="知了账号" toggleNested :open="false">
          <mu-list-item slot="nested" title="邮箱" describeText="am****@gmail.com" afterText="已验证">
          </mu-list-item>
          <mu-list-item slot="nested" title="手机" describeText="+86 132*****0102" afterText="待验证">
          </mu-list-item>
          <mu-list-item slot="nested" title="账号密码" describeText="修改密码">
          </mu-list-item>
        </mu-list-item>
        <mu-divider/>

        <mu-list-item title="社交账号" toggleNested :open="false">
          <mu-list-item disableRipple slot="nested" @click="handleToggle('weiboBound')" title="新浪微博" describeText="鲨鱼蘸酱油">
            <mu-switch v-model="weiboBound"  slot="right"/>
          </mu-list-item>
          <mu-list-item disableRipple slot="nested" @click="handleToggle('wechatBound')" title="微信" describeText="尚未绑定">
            <mu-switch v-model="wechatBound"  slot="right"/>
          </mu-list-item>
          <mu-list-item disableRipple slot="nested" @click="handleToggle('qqBound')" title="QQ" describeText="尚未绑定">
            <mu-switch v-model="qqBound"  slot="right"/>
          </mu-list-item>
        </mu-list-item>
        <mu-divider/>

        <mu-list-item title="账号安全" toggleNested :open="false">
          <mu-list-item slot="nested" title="最近活动历史" describeText="*次活动会话" afterText="已验证">
          </mu-list-item>
          <mu-list-item slot="nested" title="手机" describeText="+86 132*****0102" afterText="待验证">
          </mu-list-item>
          <mu-list-item slot="nested" title="账号密码" describeText="修改密码">
          </mu-list-item>
        </mu-list-item>
        <mu-divider/>
      </mu-list>


      <mu-list class="more-lists-content">
        <mu-sub-header>关于与帮助</mu-sub-header>
        <mu-list-item title="意见反馈">
          <mu-icon slot="left" value="send"/>
        </mu-list-item>
        <mu-divider/>
        <mu-list-item title="开源许可">
          <mu-icon slot="left" value="devices"/>
        </mu-list-item>
        <mu-divider/>
        <mu-list-item title="知了协议">
          <mu-icon slot="left" value="dvr"/>
        </mu-list-item>
        <mu-divider/>
      </mu-list>

      <mu-list class="more-lists-content">
        <mu-sub-header>切换主题</mu-sub-header>
        <!--<mu-list-item>-->
        <mu-list-item disableRipple title="切换主题">
          <mu-icon-menu slot="right" icon="more_vert" :value="theme" @change="changeTheme">
            <mu-menu-item title="天际蓝" value="light" />
            <mu-menu-item title="魅惑紫" value="purple" />
            <mu-menu-item title="深空灰" value="carbon" />
            <mu-menu-item title="深井绿" value="teal" />
          </mu-icon-menu>
        </mu-list-item>
        <mu-list-item disableRipple title="夜间模式">
          <mu-switch v-model="isNightMode" @change="nightMode" slot="right"/>
        </mu-list-item>
        <mu-divider/>
      </mu-list>

      <mu-list class="more-lists-content">
        <mu-sub-header>联系作者</mu-sub-header>
        <mu-list-item title="amosannn@gmail.com" describeText="电子邮箱">
          <mu-icon value="email" color="indigo" slot="left"/>
          <!--<mu-icon value="chat_bubble" slot="right"/>-->
        </mu-list-item>
      </mu-list>
      <mu-divider/>

      <mu-list class="more-lists-content">
        <mu-list-item title="退出登录" class="more-logout" titleClass="more-logout-title"/>
      </mu-list>
    </section>

  </div>
</template>

<script>
  import light from '!raw-loader!muse-ui/dist/theme-light.css'
  import purple from '!raw-loader!muse-ui/dist/theme-default.css'
  import dark from '!raw-loader!muse-ui/dist/theme-dark.css'
  import carbon from '!raw-loader!muse-ui/dist/theme-carbon.css'
  import teal from '!raw-loader!muse-ui/dist/theme-teal.css'
  import zhiliao from '@/components/header/header.vue'
  export default {
		name: "more",
    components:{
      zhiliao
    },
    data () {
      return {
        user: null,
        events: false,
        calls: false,
        messages: false,
        notifications: false,
        sounds: false,
        videoSounds: false,
        weiboBound: true,
        wechatBound: false,
        qqBound: false,
        isNightMode: false,
        theme: this.getCookie('theme')?this.getCookie('theme'):'carbon',
        themes: {
          light,
          purple,
          dark,
          carbon,
          teal
        }
      }
    },
    mounted() {
		  this.getData();
    },
    methods: {
		  getData(){
        this.axios.post('http://127.0.0.1:8080/zhiliao/profile/0',{
          page: 1
        }).then( (response) => {
          if( response.data.code === '0000'){
            this.user = response.data.data.user;
          }
        })
      },
      handleToggle (key) {
        this[key] = !this[key]
      },
      nightMode (isNight) {
        console.log("is night "+this.isNightMode+"  "+ isNight);
        if(isNight === true) {
          // let oldTheme = this.getCookie('theme');
          let expireDays = 1000 * 60 * 60 * 24 * 15;
          // this.setCookie('old_theme', oldTheme, expireDays);
          this.setCookie('theme', 'dark', expireDays);
          this.changeTheme('dark');
          this.isNightMode = true;

        } else if(isNight === false) {
          let theme = this.getCookie('old_theme');
          this.delCookie('old_theme');
          // let expireDays = 1000 * 60 * 60 * 24 * 15;
          // this.setCookie('theme', theme, expireDays);
          this.changeTheme(theme);
          this.isNightMode = false;
        }
      },
      changeTheme (theme) {
        this.theme = theme
        const styleEl = this.getThemeStyle()
        styleEl.innerHTML = this.themes[theme] || ''
      },
      getThemeStyle () {
        const themeId = 'muse-theme'
        let styleEl = document.getElementById(themeId)
        if (styleEl) return styleEl
        styleEl = document.createElement('style')
        styleEl.id = themeId
        document.body.appendChild(styleEl)
        return styleEl
      },
      // 我的收藏
      jumpToCollection() {
        this.$router.push("/collection");
      },
      jumpToProfile(){
		    this.$router.push("/profile/"+this.user.userId);
      }
    },
	}
</script>

<style lang="less" scoped>
  .title{
    text-align: center;
    height: 1rem;
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    z-index: 10;
    .appbar-text{
      font-size: .1rem;
    }
    /*.appbar-search-block{*/
    /*font-size: 18px;*/
    /*margin-left: -8px;*/
    /*margin-bottom: 2px;*/
    /*}*/
  }

  .more-lists{
    margin-top: 1.1rem;
    /*margin-bottom: 1.5rem;*/
    height: calc(100vh - 2.5rem);
    overflow-y: scroll;
    overflow-x: hidden;
    /*overflow: auto;*/
    .more-lists-content{
      margin-bottom: .5rem
    }
    .more-logout{
      text-align: center;
      /*color: #ff3c27;*/
    }
  }
</style>

<style lang="less">
  .more-logout-title{
    color: #ff3c27;
  }
</style>
