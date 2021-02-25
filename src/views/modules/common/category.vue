<template>
  <div>
    <el-tree
      :data="menus"
      :props="defaultProps"
      node-key="catId"
      ref="menuTree"
      @node-click="nodeClick"
    >
    </el-tree>
  </div>
</template>

<script>
export default {
  data() {
    return {
      expandKey: [],
      menus: [],
      defaultProps: {
        children: "children",
        label: "name",
      },
    };
  },
  methods: {
    getMenus() {
      this.$http({
        url: this.$http.adornUrl("/product/pmscategory/list/tree"),
        method: "get",
      }).then(({ data }) => {
        console.log("成功获取到菜单数据.....", data.data);
        this.menus = data.data;
      });
    },
    //节点带年纪事件
    nodeClick(data, Node, component) {
      console.log("子组件category节点被点击", data, Node, component);
      //向父组件发送数据
      this.$emit("tree-node-click",data, Node, component);
    },
  },
  //生命周期 创建完成可以访问当前this实例
  created() {
    this.getMenus();
  },
  //生命周期 挂载完成，可以访问Dom 元素
  mounted() {},
  //生命周期 创建之前
  beforeCreate() {},
  //生命周期 挂载之前
  beforeMount() {},
  //生命周期 更新之前
  beforeUpdate() {},
  //生命周期 更新之后
  update() {},
  //生命周期 销毁之前
  beforeDestory() {},
  //生命周期 销毁之后
  destoryed() {},
  //如果页面有keep-alive 功能此函数会被触发
  activated() {},
};
</script>
