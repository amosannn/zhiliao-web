<template>
  <mu-paper class="foot_nav">
    <mu-bottom-nav :value="bottomNav" @change="handleChange">
      <mu-bottom-nav-item to="/" value="home" title="首页" icon="library_books"/>
      <!--<mu-bottom-nav-item to="/answer" value="answer" title="回答" icon="border_color"/>-->
      <mu-bottom-nav-item to="/collection" value="collection" title="收藏夹" icon="archive"/>
      <mu-bottom-nav-item value="me" title="我的" icon="face"/>
      <mu-bottom-nav-item value="notification" title="通知" icon="notifications"/>
      <mu-bottom-nav-item to="/more" value="more" title="更多" icon="menu"/>
    </mu-bottom-nav>
  </mu-paper>
</template>

<script>
	export default {
		name: "foot-nav"
	}
</script>

<style lang="less" scoped>
  .foot_nav{
    position: fixed;
    bottom: 0;
    left: 0;
    right: 0;
    /*display: flex;*/
  }
</style>
