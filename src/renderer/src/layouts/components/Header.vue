<template>
  <div class="titlebar" @mousedown.self="handleMouseDown">
    <div class="left no-drag system-functions">
      <history-control class="system-function" />
      <search-bar class="system-function" />
      <player-show class="system-function" />
    </div>
    <div class="right no-drag">
      <div class="system-functions">
        <sponsor class="system-function" />
        <language class="system-function" />
        <system-skin class="system-function" />
        <lab class="system-function" />
        <system-config class="system-function" />
        <system-pin class="system-function" />
      </div>
      <system-control class="window" />
    </div>
  </div>
</template>

<script setup lang="ts">
import HistoryControl from './HistoryControl.vue';
import Language from './Language.vue';
import PlayerShow from './PlayShow.vue';
import SearchBar from './SearchBar.vue';
import Sponsor from './Sponsor.vue';
import SystemConfig from './SystemConfig.vue';
import SystemControl from './SystemControl.vue';
import SystemSkin from './SystemSkin.vue';
import SystemPin from './SystemPin.vue';
import Lab from './Lab.vue';

const handleMouseDown = (event) => {
  if (event.detail === 2) {
    window.electron.ipcRenderer.send('win:invoke', 'max');
  }
}
</script>

<style lang="less" scoped>
.titlebar {
  -webkit-app-region: drag;
  display: flex;
  justify-content: space-between;
  width: 100%;
  height: 56px;
  padding: var(--td-comp-margin-m) var(--td-comp-margin-xs) var(--td-comp-margin-m) 0;

  .no-drag {
    -webkit-app-region: no-drag;
  }

  .mg-left {
    margin-left: var(--td-comp-margin-l);
  }

  .left, .right {
    display: flex;
    flex-direction: row;
    align-items: center;
    gap: var(--td-comp-margin-l);

    .system-functions {
      display: flex;
      align-items: center;
      justify-content: space-around;
      background: var(--td-bg-color-container);
      border-radius: var(--td-radius-default);

      &>.system-function:first-of-type {
        margin-left: 0;
      }

      .system-function {
        margin-left: var(--td-comp-margin-xs);
        width: 32px;
        height: 32px;
        display: flex;
        align-items: center;
        justify-content: center;

        :deep(.t-button) {
          &:not(.t-is-disabled):not(.t-button--ghost) {
            --ripple-color: transparent;
          }
        }

        :deep(.t-button__text) {
          svg {
            color: var(--td-text-color-placeholder);
          }
        }

        :deep(.t-button--variant-text) {
          &:hover {
            border-color: transparent;
            background-color: transparent;

            .t-button__text {
              svg {
                color: var(--td-primary-color);
              }
            }
          }
        }
      }
    }
  }
}
</style>
