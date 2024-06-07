<template>
  <div v-show="terminal_display">
    <div class="overlay">
      <div class="terminal">
        <div class="terminal-header">
          <span>终端: 消息 来自 {{ from_title }}<a @click="click_clicked">关闭</a></span>
        </div>
        <div class="terminal-body" ref="terminalBody" align="left" style="line-height:1.1;">
          <p style="line-height:1.7;">
            <!-- 开头的版权字符 可以随意修改或者直接删除-->
            *******************************<br>
            ****** <Your Name> **************<br>
            ****** <Another Things> *********<br>
            *******************************<br>
          </p>
          <p v-for="(line, index) in terminalLines" :key="index">
            {{ line }}
          </p>
        </div>
      </div>
    </div>
  </div>
  <div id="inlet">
    <Icon icon="icon-park:birthday-cake" style="font-size: 30px" @click="cake_has_clicked" />
  </div>
</template>

<script setup>
import { Icon } from '@iconify/vue';
import {nextTick, ref} from 'vue';
import axios from 'axios';

const terminal_display = ref(false);
// 这里是标题栏的来自xxxx的消息中的消息来源 可随意更改
const from_title = ref('?????');
const terminalLines = ref([]);
const terminalBody = ref(null);
let intervalId = null;
let contentIndex = 0;


async function cake_has_clicked() {
  terminal_display.value = true;
  <!--  你需要将这里替换为一个允许跨域且句式为换行符分隔的txt文件-->
  const response = await axios.get('<http_address_to_text_file>', {
    responseType: 'text',
  });
  const contentLines = response.data.split('\n');
  setInterval(() => {
    if (contentIndex < contentLines.length) {
      terminalLines.value.push(contentLines[contentIndex]);
      contentIndex++;
      nextTick(() => {
        terminalBody.value.scrollTop = terminalBody.value.scrollHeight;
      });
    } else if (intervalId !== null) {
      clearInterval(intervalId);
      intervalId = null;
      terminalLines.value.push('完毕');
    }
  }, 2000);
}

function click_clicked() {
  terminal_display.value = false;
}
</script>

<style scoped>
.overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.7);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
}

.terminal {
  background-color: black;
  color: white;
  width: 600px;
  height: 450px;
  border-radius: 8px;
  box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.3);
}

.terminal-header {
  background-color: #333;
  padding: 10px;
  border-top-left-radius: 8px;
  border-top-right-radius: 8px;
}

.terminal-header span {
  font-size: 18px;
  font-weight: bold;
}

.terminal-body {
  padding: 20px;
  height: calc(100% - 60px);
  overflow-y: auto;
}
</style>
