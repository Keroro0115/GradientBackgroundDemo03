<template>
  <div class="gradient-background" ref="backgroundRef">
    <!-- 紫色椭圆形大球 -->
    <div 
      class="gradient-orb purple-orb"
      :style="purpleOrbStyle"
    ></div>
    
    <!-- 蓝色正方形小球 -->
    <div 
      class="gradient-orb blue-orb"
      :style="blueOrbStyle"
    ></div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue'

const backgroundRef = ref(null)
const mousePosition = ref({ x: 0, y: 0 })
const time = ref(0)

// 紫色球体初始位置和样式
const purpleOrbStyle = computed(() => {
  const baseX = 50 // 回到中心偏左
  const baseY = 30
  
  // 静态波动效果 - 缓慢优雅的波动
  const waveX = Math.sin(time.value * 0.0008) * 15 + Math.sin(time.value * 0.0012) * 8
  const waveY = Math.cos(time.value * 0.0006) * 12 + Math.cos(time.value * 0.0014) * 6
  
  // 鼠标交互效果
  const mouseInfluence = 0.2
  const deltaX = (mousePosition.value.x - baseX) * mouseInfluence
  const deltaY = (mousePosition.value.y - baseY) * mouseInfluence
  
  const finalX = baseX + waveX + deltaX
  const finalY = baseY + waveY + deltaY
  
  // 限制在背景范围内
  const constrainedX = Math.max(0, Math.min(100, finalX))
  const constrainedY = Math.max(0, Math.min(100, finalY))
  
  // 液态变形效果 - 缓慢的呼吸和变形
  const breathScale = 1 + Math.sin(time.value * 0.0005) * 0.15 // 呼吸效果
  const liquidDeform = Math.sin(time.value * 0.0007) * 0.3 // 液态变形
  const rotation = Math.sin(time.value * 0.0003) * 8 // 缓慢旋转
  
  // 动态形状变化 - 从椭圆到圆形再到液态
  const shapePhase = Math.sin(time.value * 0.0004) // 形状变化相位
  let borderRadius = ''
  
  if (shapePhase > 0.5) {
    // 圆形状态
    borderRadius = '50%'
  } else if (shapePhase > 0) {
    // 椭圆状态
    borderRadius = '60% 40% 70% 30% / 40% 60% 30% 70%'
  } else if (shapePhase > -0.5) {
    // 液态状态
    borderRadius = '70% 30% 60% 40% / 50% 70% 30% 60%'
  } else {
    // 扩散状态
    borderRadius = '80% 20% 70% 30% / 30% 80% 20% 70%'
  }
  
  return {
    left: `${constrainedX}%`,
    top: `${constrainedY}%`,
    transform: `translate(-50%, -50%) rotate(${rotation}deg) scale(${breathScale + liquidDeform})`,
    width: '330px',
    height: '236px',
    background: 'linear-gradient(100deg, rgba(9, 9, 9, 0.3) 0%, rgba(111, 0, 255, 0.4) 100%)',
    filter: 'blur(100px)',
    borderRadius: borderRadius
  }
})

// 蓝色球体初始位置和样式
const blueOrbStyle = computed(() => {
  const baseX = 55 // 靠近紫色球体，相偎相依
  const baseY = 50 // 稍微偏下一点
  
  // 静态波动效果 - 缓慢优雅的波动，与紫色球体协调
  const waveX = Math.sin(time.value * 0.0011) * 18 + Math.cos(time.value * 0.0009) * 10
  const waveY = Math.cos(time.value * 0.0007) * 15 + Math.sin(time.value * 0.0013) * 8
  
  // 鼠标交互效果
  const mouseInfluence = 0.25
  const deltaX = (mousePosition.value.x - baseX) * mouseInfluence
  const deltaY = (mousePosition.value.y - baseY) * mouseInfluence
  
  const finalX = baseX + waveX + deltaX
  const finalY = baseY + waveY + deltaY
  
  // 限制在背景范围内
  const constrainedX = Math.max(0, Math.min(100, finalX))
  const constrainedY = Math.max(0, Math.min(100, finalY))
  
  // 液态变形效果 - 缓慢的呼吸和变形
  const breathScale = 1 + Math.cos(time.value * 0.0006) * 0.12 // 呼吸效果，与紫色球体相反
  const liquidDeform = Math.cos(time.value * 0.0008) * 0.25 // 液态变形
  const rotation = Math.cos(time.value * 0.0004) * 6 // 缓慢旋转
  
  // 动态形状变化 - 与紫色球体不同步的形状变化
  const shapePhase = Math.cos(time.value * 0.0005) // 形状变化相位
  let borderRadius = ''
  
  if (shapePhase > 0.5) {
    // 椭圆状态
    borderRadius = '50% 30% 60% 40% / 30% 50% 40% 60%'
  } else if (shapePhase > 0) {
    // 圆形状态
    borderRadius = '50%'
  } else if (shapePhase > -0.5) {
    // 扩散状态
    borderRadius = '60% 40% 80% 20% / 40% 60% 20% 80%'
  } else {
    // 液态状态
    borderRadius = '70% 30% 50% 50% / 50% 70% 30% 50%'
  }
  
  return {
    left: `${constrainedX}%`,
    top: `${constrainedY}%`,
    transform: `translate(-50%, -50%) rotate(${rotation}deg) scale(${breathScale + liquidDeform})`,
    width: '160px',
    height: '160px',
    background: 'linear-gradient(69deg, rgba(39, 75, 202, 0.3) 0%, rgba(255, 255, 255, 0.2) 100%)',
    filter: 'blur(200px)',
    borderRadius: borderRadius
  }
})

// 鼠标移动处理
const handleMouseMove = (event) => {
  if (!backgroundRef.value) return
  
  const rect = backgroundRef.value.getBoundingClientRect()
  const x = ((event.clientX - rect.left) / rect.width) * 100
  const y = ((event.clientY - rect.top) / rect.height) * 100
  
  // 优雅的缓动效果
  mousePosition.value = { 
    x: mousePosition.value.x + (x - mousePosition.value.x) * 0.08,
    y: mousePosition.value.y + (y - mousePosition.value.y) * 0.08
  }
}

// 鼠标离开处理
const handleMouseLeave = () => {
  // 平滑回到中心位置
  const targetX = 50
  const targetY = 50
  const animateBack = () => {
    const dx = targetX - mousePosition.value.x
    const dy = targetY - mousePosition.value.y
    
    if (Math.abs(dx) > 0.1 || Math.abs(dy) > 0.1) {
      mousePosition.value = {
        x: mousePosition.value.x + dx * 0.03,
        y: mousePosition.value.y + dy * 0.03
      }
      requestAnimationFrame(animateBack)
    }
  }
  animateBack()
}

// 动画循环
let animationId = null
const animate = () => {
  time.value = Date.now()
  animationId = requestAnimationFrame(animate)
}

onMounted(() => {
  animate()
  if (backgroundRef.value) {
    backgroundRef.value.addEventListener('mousemove', handleMouseMove)
    backgroundRef.value.addEventListener('mouseleave', handleMouseLeave)
  }
})

onUnmounted(() => {
  if (animationId) {
    cancelAnimationFrame(animationId)
  }
  if (backgroundRef.value) {
    backgroundRef.value.removeEventListener('mousemove', handleMouseMove)
    backgroundRef.value.removeEventListener('mouseleave', handleMouseLeave)
  }
})
</script>

<style scoped>
.gradient-background {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
  pointer-events: none;
  z-index: 1;
}

.gradient-orb {
  position: absolute;
  pointer-events: none;
  will-change: transform, filter;
  transition: all 0.4s cubic-bezier(0.25, 0.46, 0.45, 0.94);
  animation-timing-function: ease-in-out;
}

.purple-orb {
  opacity: 0.6;
  mix-blend-mode: soft-light;
  filter: blur(100px) saturate(1.2);
}

.blue-orb {
  opacity: 0.5;
  mix-blend-mode: soft-light;
  filter: blur(200px) saturate(1.1);
}

/* 确保背景不会超出容器 */
.gradient-background::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: transparent;
  pointer-events: auto;
}

/* 添加优雅的生命力效果 */
.purple-orb::before {
  content: '';
  position: absolute;
  top: -20px;
  left: -20px;
  right: -20px;
  bottom: -20px;
  background: inherit;
  border-radius: inherit;
  filter: blur(60px);
  opacity: 0.3;
  animation: gentlePulse 8s ease-in-out infinite;
}

.blue-orb::before {
  content: '';
  position: absolute;
  top: -15px;
  left: -15px;
  right: -15px;
  bottom: -15px;
  background: inherit;
  border-radius: inherit;
  filter: blur(80px);
  opacity: 0.2;
  animation: gentlePulse 10s ease-in-out infinite reverse;
}

@keyframes gentlePulse {
  0%, 100% {
    transform: scale(1);
    opacity: 0.3;
  }
  50% {
    transform: scale(1.05);
    opacity: 0.1;
  }
}
</style>
