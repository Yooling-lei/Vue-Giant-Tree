<!--  -->
<template>
  <div class="box">
    <a-row>
      <a-col :span="12">
        <z-tree
          tree-id="tree-001"
          :setting="treeSetting"
          :nodes="state.treeData"
          @onClick="onClick"
          @onDrag="onDrag"
        />
      </a-col>
      <a-col :span="12">
        <z-tree
          tree-id="tree-002"
          :setting="treeSetting"
          :nodes="state.treeData"
          @onClick="onClick"
      /></a-col>
    </a-row>
  </div>
</template>

<script>
import { reactive } from "vue";
import { message } from "ant-design-vue";
import zTree from "../components/zTree.vue";
//问题

const bigData = require("@/mock/big-tree.json");

export default {
  name: "index",
  props: {},
  components: {
    zTree,
  },
  setup() {
    const state = reactive({
      treeData: bigData.data,
    });

    let disable = false;
    setTimeout(() => {
      disable = false;
      message.info("wwwwwwwwwwww");
    }, 10000);

    /** 拖拽到目标节点时,设置是否允许移动到目标节点前面 */
    const dragPre = () => {
      if (disable) return false;
      return true;
    };

    /**拖拽到目标节点时,设置是否允许移动到目标节点后面 */
    const dragNext = () => {
      if (disable) return false;

      return true;
    };
    /** 拖拽到目标节点时,设置是否允许称为目标节点的子节点 */
    const dragInner = () => {
      if (disable) return false;

      return true;
    };

    return {
      state,
      //点击事件
      onClick: (e, treeId, treeNode) => {
        console.log(e.type, treeId, treeNode);
      },
      /**
       *
       * @param {*} e
       * @param {String} treeId 被拖拽的节点的id
       * @param {Array} treeNodes
       */
      onDrag: (e, treeId, treeNodes) => {
        console.log(treeId, treeNodes);
      },

      //树的设置
      treeSetting: {
        data: {
          simpleData: {
            enable: true,
            pIdKey: "pid",
          },
        },
        view: {
          showIcon: false,
        },
        edit: {
          enable: true,
          drag: {
            prev: dragPre,
            next: dragNext,
            inner: dragInner,
          },
        },
      },
    };
  },
};
</script>
<style scoped></style>
