<template>
  <div
    class="macos-window"
    :class="{ 'macos-window-active': isActive }"
    :style="windowStyle"
    @mousedown="activateWindow"
  >
    <!-- 窗口标题栏 -->
    <div
      class="window-titlebar"
      @mousedown.prevent="startDrag"
      @dblclick="toggleMaximize"
    >
      <!-- 窗口控制按钮 -->
      <div class="window-controls">
        <button
          class="control-button close"
          @click.stop="$emit('close')"
          title="关闭"
        >
          <span>×</span>
        </button>
        <button
          class="control-button minimize"
          @click.stop="$emit('minimize')"
          title="最小化"
        >
          <span>−</span>
        </button>
        <button
          class="control-button maximize"
          @click.stop="toggleMaximize"
          title="最大化"
        >
          <span>+</span>
        </button>
      </div>

      <!-- 窗口标题 -->
      <div class="window-title">
        {{ title }}
      </div>

      <!-- 右侧工具区域 -->
      <div class="window-tools">
        <slot name="tools"></slot>
      </div>
    </div>

    <!-- 窗口内容区域 -->
    <div class="window-content">
      <slot></slot>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted, onUnmounted } from "vue";

// 定义组件属性
const props = defineProps({
  title: {
    type: String,
    default: "Untitled Window",
  },
  width: {
    type: [Number, String],
    default: 600,
  },
  height: {
    type: [Number, String],
    default: 400,
  },
  x: {
    type: Number,
    default: 50,
  },
  y: {
    type: Number,
    default: 50,
  },
  resizable: {
    type: Boolean,
    default: true,
  },
  active: {
    type: Boolean,
    default: true,
  },
});

// 定义事件
const emit = defineEmits([
  "close",
  "minimize",
  "maximize",
  "restore",
  "move",
  "resize",
  "activate",
]);

// 窗口状态
const isActive = ref(props.active);
const isMaximized = ref(false);
const position = ref({ x: props.x, y: props.y });
const size = ref({ width: props.width, height: props.height });
const originalSize = ref(null);
const originalPosition = ref(null);

// 拖拽状态
const isDragging = ref(false);
const dragOffset = ref({ x: 0, y: 0 });

// 计算窗口样式
const windowStyle = computed(() => {
  const style = {
    width:
      typeof size.value.width === "number"
        ? `${size.value.width}px`
        : size.value.width,
    height:
      typeof size.value.height === "number"
        ? `${size.value.height}px`
        : size.value.height,
  };

  if (!isMaximized.value) {
    style.transform = `translate(${position.value.x}px, ${position.value.y}px)`;
  }

  return style;
});

// 激活窗口
function activateWindow() {
  isActive.value = true;
  emit("activate");
}

// 开始拖拽
function startDrag(event) {
  if (isMaximized.value) return;

  isDragging.value = true;
  dragOffset.value = {
    x: event.clientX - position.value.x,
    y: event.clientY - position.value.y,
  };

  document.addEventListener("mousemove", onDrag);
  document.addEventListener("mouseup", stopDrag);
}

// 拖拽中
function onDrag(event) {
  if (!isDragging.value) return;

  position.value = {
    x: event.clientX - dragOffset.value.x,
    y: event.clientY - dragOffset.value.y,
  };

  emit("move", position.value);
}

// 停止拖拽
function stopDrag() {
  isDragging.value = false;
  document.removeEventListener("mousemove", onDrag);
  document.removeEventListener("mouseup", stopDrag);
}

// 切换最大化状态
function toggleMaximize() {
  if (isMaximized.value) {
    // 恢复窗口
    isMaximized.value = false;
    if (originalSize.value && originalPosition.value) {
      size.value = { ...originalSize.value };
      position.value = { ...originalPosition.value };
    }
    emit("restore", { size: size.value, position: position.value });
  } else {
    // 最大化窗口
    originalSize.value = { ...size.value };
    originalPosition.value = { ...position.value };
    isMaximized.value = true;
    emit("maximize");
  }
}

// 组件挂载和卸载时的清理
onMounted(() => {
  window.addEventListener("mousedown", handleOutsideClick);
});

onUnmounted(() => {
  window.removeEventListener("mousedown", handleOutsideClick);
  document.removeEventListener("mousemove", onDrag);
  document.removeEventListener("mouseup", stopDrag);
});

// 处理窗口外点击
function handleOutsideClick(event) {
  const windowEl = event.target.closest(".macos-window");
  if (!windowEl && isActive.value) {
    isActive.value = false;
  }
}
</script>

<style scoped>
.macos-window {
  position: absolute;
  display: flex;
  flex-direction: column;
  background-color: rgba(255, 255, 255, 0.8);
  backdrop-filter: blur(10px);
  border-radius: 10px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
  overflow: hidden;
  transition: box-shadow 0.2s ease;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  z-index: 10;
}

.macos-window-active {
  z-index: 100;
  box-shadow: 0 15px 40px rgba(0, 0, 0, 0.3);
}

.window-titlebar {
  display: flex;
  align-items: center;
  height: 38px;
  padding: 0 12px;
  background: linear-gradient(to bottom, #f9f9f9, #e4e4e4);
  border-bottom: 1px solid #d1d1d1;
  border-top-left-radius: 10px;
  border-top-right-radius: 10px;
  user-select: none;
  cursor: default;
}

.window-controls {
  display: flex;
  gap: 8px;
  margin-right: 8px;
}

.control-button {
  width: 12px;
  height: 12px;
  border-radius: 50%;
  border: none;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  position: relative;
}

.control-button span {
  font-size: 14px;
  line-height: 1;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  opacity: 0;
  transition: opacity 0.1s ease;
}

.control-button:hover span {
  opacity: 1;
}

.control-button.close {
  background-color: #fe11c5;
}

.control-button.minimize {
  background-color: #ffbd2e;
}

.control-button.maximize {
  background-color: #28c940;
}

.window-title {
  flex: 1;
  text-align: center;
  font-size: 13px;
  color: #4d4d4d;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.window-tools {
  margin-left: 8px;
}

.window-content {
  flex: 1;
  overflow: auto;
  background-color: white;
  position: relative;
}

/* 最大化状态 */
.macos-window.maximized {
  border-radius: 0;
  width: 100% !important;
  height: 100% !important;
  transform: none !important;
  top: 0 !important;
  left: 0 !important;
}

.macos-window.maximized .window-titlebar {
  border-radius: 0;
}
</style>
