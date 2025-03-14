<!--
  * Name: VideoMediaControl Video media operation component (on/off camera)
  * @param hasMore boolean Whether to display the [More] icon，which can switch camera
  * @param isMuted boolean Whether the video is muted or not
  * @param isDisabled boolean Whether the video is disabled or not
  * Usage:
  * Use <video-media-control :isMuted="isMuted" /> in the template
  *
  * 名称: VideoMediaControl 视频媒体操作组件（开关摄像头）
  * @param hasMore boolean 是否展示【更多】icon, 可以切换摄像头
  * @param isMuted boolean 视频是否被静画状态
  * @param isDisabled boolean 视频是否 disabled 状态
  * 使用方式：
  * 在 template 中使用 <video-media-control :isMuted="isMuted" />
-->
<template>
  <div>
    <div class="video-control-container">
      <icon-button
        :title="t('Camera')"
        :has-more="hasMore"
        :disabled="isDisabled"
        :is-not-support="!isSupportVideoMedia"
        @click-icon="handleClickIcon"
        @click-more="handleMore"
      >
        <svg-icon style="display: flex" :icon="icon" size="24"></svg-icon>
      </icon-button>
      <video-setting-tab
        v-if="showVideoSettingTab"
        class="video-tab"
        :with-mirror="true"
        theme="white"
      ></video-setting-tab>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, computed, Ref } from 'vue';
import IconButton from '../common/base/IconButton.vue';
import TUIMessageBox from '../common/base/MessageBox/index';
import SvgIcon from './base/SvgIcon.vue';
import VideoSettingTab from '../common/VideoSettingTab.vue';
import { useI18n } from '../../locales';
import { isGetUserMediaSupported, isEnumerateDevicesSupported } from '../../utils/mediaAbility';

interface Props {
  hasMore?: boolean,
  isMuted: boolean,
  isDisabled?: boolean,
}

const props = withDefaults(defineProps<Props>(), {
  hasMore: true,
  isMuted: undefined,
  isDisabled: false,
});

const emits = defineEmits(['click']);

const { t } = useI18n();
const showVideoSettingTab: Ref<boolean> = ref(false);
const isSupportVideoMedia = isGetUserMediaSupported && isEnumerateDevicesSupported;

const icon = computed(() => (props.isMuted ? 'CameraOffIcon' : 'CameraOnIcon'));

async function handleClickIcon() {
  if (!isSupportVideoMedia) {
    TUIMessageBox({
      title: t('Note'),
      message: t('The current browser does not support capturing video'),
      appendToRoomContainer: true,
      confirmButtonText: t('Sure'),
    });
    return;
  }
  emits('click');
  showVideoSettingTab.value = false;
}

function handleMore() {
  showVideoSettingTab.value = !showVideoSettingTab.value;
}

function handleHideVideoSettingTab() {
  if (showVideoSettingTab.value) {
    showVideoSettingTab.value = false;
  }
}

</script>

<style lang="scss" scoped>

$videoTabWidth: 305px;

.video-control-container {
  position: relative;
  .video-tab {
    position: absolute;
    left: -5px;
    width: $videoTabWidth;
    background: #FFFFFF;
    padding: 20px 20px 24px 20px;
    border-radius: 8px;
    box-shadow:
      0px 2px 4px -3px rgba(32, 77, 141, 0.03),
      0px 6px 10px 1px rgba(32, 77, 141, 0.06),
      0px 3px 14px 2px rgba(32, 77, 141, 0.05);
    &::before {
      position: absolute;
      left: 30px;
      bottom: -10px;
      border-top: 5px solid #FFFFFF;
      border-left: 5px solid transparent;
      border-right: 5px solid transparent;
      border-bottom: 5px solid transparent;
    }
  }
}
</style>
