<template>
  <div>
    <Layout>
      <Sider hide-trigger style="height:100vh">
        <div><router-link to="/content/list1">新闻1</router-link></div>
        <div>
          <router-link to="/content/list2">新闻2</router-link>
        </div>
      </Sider>
      <Layout>
        <Header>user</Header>
        <Content> <router-view /></Content>
      </Layout>
    </Layout>
  </div>
</template>

<script>
export default {
  name: "layout"
};
</script>

<style>
.gw-header {
  height: 60px;
  border: 1px solid #f0f;
}
</style>
