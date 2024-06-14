<!-- eslint-disable vue/no-v-html -->
<!-- eslint-disable vue/max-attributes-per-line -->
<!-- eslint-disable vue/html-self-closing -->
<template>
  <div>
    <input
      v-if="node.isEditing"
      ref="editCtrl"
      v-model="nodeText"
      type="text"
      class="tree-input"
      @blur="stopEditing"
      @keyup.enter="stopEditing"
      @mouseup.stop
    />
    <span v-else v-html="node.text"></span>
  </div>
</template>

<script>
import { ref, onMounted } from "vue";

export default {
  name: "NodeContent",
  props: {
    node: {
      type: Object,
      required: true
    }
  },
  setup(props) {
    const nodeText = ref(props.node.text);
    const editCtrl = ref(null);

    const stopEditing = () => {
      props.node.stopEditing(nodeText.value);
    };

    onMounted(() => {
      if (props.node.isEditing) {
        editCtrl.value.focus();
      }
    });

    return {
      nodeText,
      editCtrl,
      stopEditing
    };
  }
};
</script>
