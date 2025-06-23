<script setup lang="ts">
import {ref} from "vue";
import {marked} from "marked";
import DOMPurify from 'dompurify'
import DefaultMsg from './default_msg.md?raw'
import hljs from 'highlight.js';

const input = ref(DefaultMsg)

const switchShow = ref(false)

function switchChange(bl: boolean) {
  if (!bl) return
  const mark = marked.parse(input.value)
  const showMark = document.getElementById('showMark')
  if (!showMark) return;
  if (typeof (mark) === 'string') {
    strToElement(showMark, mark)
  } else {
    mark.then(mk => {
      strToElement(showMark, mk)
    })
  }
}

function strToElement(showMark: HTMLElement, element: string) {
  element = DOMPurify.sanitize(element)
  let parser = new DOMParser();
  let doc = parser.parseFromString(element, 'text/html');
  for (const preTag of doc.body.getElementsByTagName('pre')) {
    highlightCode(preTag)
  }
  showMark.innerHTML = doc.body.innerHTML
}

function highlightCode(element: HTMLElement) {
  hljs.highlightElement(element)
}
</script>

<template>
  <div class="box">
    <el-card class="card">
      <el-form>
        <el-form-item label="输入/预览">
          <el-switch v-model="switchShow" @change="switchChange"/>
        </el-form-item>
        <el-form-item>
          <el-scrollbar height="calc(100vh - 150px)" style="width: 100%">
            <el-input v-show="!switchShow" v-model="input" type="textarea" :autosize="{minRows:35, maxRows:400}"/>
            <article v-show="switchShow" id="showMark" class="markdown-body"/>
          </el-scrollbar>
        </el-form-item>
      </el-form>
    </el-card>
  </div>
</template>

<style scoped>
.box {
  display: block;
  justify-content: center;
  align-items: center;
}

.card {
  min-height: calc(100vh - 45px);
  margin: 20px 10px;
}

.markdown-body {
  width: auto;
}

@media (max-width: 500px) {
  .markdown-body {
    width: auto;
  }
}
</style>
