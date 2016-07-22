<template>
  <div id="app">
    <div id="panel-left" class="split split-horizontal">
      <operation-list id="tdd-operation-list"></operation-list>
    </div>
    <div id="panel-right" class="split split-horizontal">
      <preview id="tdd-preview" :url="'https://www.github.com/'"></preview>
    </div>
  </div>
</template>

<script>
import split from 'split.js'
import Hello from './components/Hello'
import OperationList from './components/OperationList'
import Preview from './components/Preview'

export default {
  components: {
    Hello, OperationList, Preview
  },

  ready () {
    console.log(document.getElementById('panel-left'), document.getElementById('panel-right'))
    split(['#panel-left', '#panel-right'])
  }
}
</script>

<style>
  html, body, #app {
    height: 100%;
  }

  body {
    margin: 0;
  }

  #tdd-preview {
    height: 100%;
  }

  .split {
    -webkit-box-sizing: border-box;
       -moz-box-sizing: border-box;
            box-sizing: border-box;

    overflow-y: auto;
    overflow-x: hidden;
  }

  .content {
    border: 1px solid #C0C0C0;
    box-shadow: inset 0 1px 2px #e4e4e4;
    background-color: #fff;
  }

  .gutter {
    background-repeat: no-repeat;
    background-position: 50%;
    background-color: #eee;
  }

  .gutter.gutter-horizontal {
    cursor: col-resize;
    background-image: url('/static/images/vertical.png');
  }

  .gutter.gutter-vertical {
    cursor: row-resize;
    background-image: url('/static/images/horizontal.png');
  }

  .split.split-horizontal, .gutter.gutter-horizontal {
    height: 100%;
    float: left;
  }
</style>
