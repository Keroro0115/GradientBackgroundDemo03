<template>
  <div class="app">
    <!-- 主内容区域 -->
    <main class="main-content">
      <div class="content-container">
        <div class="header-section">
          <h1 class="main-title">What would you like to create today?</h1>
          <p class="subtitle">Turn your moment of inspiration into one story.</p>
        </div>
        
        <!-- 输入区域 -->
        <div class="input-section">
          <div class="input-mode">
            <button class="input-mode-btn active">
              <span class="icon">📝</span>
              Input Script
            </button>
          </div>
          
          <div class="text-input-container">
            <textarea 
              class="text-input"
              placeholder="Enter your ideas or upload your script file, and the AI will intelligently adjust it based on the duration."
            ></textarea>
            <div class="input-actions">
              <button class="add-btn">+</button>
              <button class="submit-btn">→</button>
            </div>
          </div>
          
          <!-- 建议标签 -->
          <div class="suggestions">
            <button class="suggestion-tag">
              <span class="icon">⚔️</span>
              Ancient Eastern Martial World
            </button>
            <button class="suggestion-tag">
              <span class="icon">☕</span>
              A beautiful chance encounter at a café
            </button>
            <button class="suggestion-tag">
              <span class="icon">🌙</span>
              Legends of the Moon
            </button>
          </div>
        </div>
      </div>
      
      <!-- 渐变背景 -->
      <GradientBackground />
    </main>
  </div>
</template>

<script setup>
import GradientBackground from './components/GradientBackground.vue'
</script>

<style scoped>
.app {
  min-height: 100vh;
  background-color: #f8f9fa;
  position: relative;
}

.main-content {
  position: relative;
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 2rem;
}

.content-container {
  max-width: 800px;
  width: 100%;
  position: relative;
  z-index: 2;
}

.header-section {
  text-align: center;
  margin-bottom: 3rem;
  position: relative;
}

.main-title {
  font-size: 3rem;
  font-weight: 700;
  color: #1a1a1a;
  margin-bottom: 1rem;
  line-height: 1.2;
  position: relative;
  z-index: 3;
}

.subtitle {
  font-size: 1.2rem;
  color: #666;
  font-weight: 400;
  position: relative;
  z-index: 3;
}

.input-section {
  position: relative;
  z-index: 3;
}

.input-mode {
  display: flex;
  justify-content: center;
  margin-bottom: 1.5rem;
}

.input-mode-btn {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.75rem 1.5rem;
  background: #6F00FF;
  color: white;
  border: none;
  border-radius: 0.5rem;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.2s ease;
}

.input-mode-btn:hover {
  background: #5a00d4;
  transform: translateY(-1px);
}

.text-input-container {
  position: relative;
  margin-bottom: 1.5rem;
}

.text-input {
  width: 100%;
  min-height: 200px;
  padding: 1.5rem;
  border: 2px solid #e5e7eb;
  border-radius: 0.75rem;
  font-size: 1rem;
  line-height: 1.6;
  resize: vertical;
  background: white;
  transition: border-color 0.2s ease;
}

.text-input:focus {
  outline: none;
  border-color: #6F00FF;
  box-shadow: 0 0 0 3px rgba(111, 0, 255, 0.1);
}

.input-actions {
  position: absolute;
  bottom: 1rem;
  left: 1rem;
  right: 1rem;
  display: flex;
  justify-content: space-between;
  pointer-events: none;
}

.add-btn, .submit-btn {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  border: none;
  cursor: pointer;
  font-size: 1.2rem;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.2s ease;
  pointer-events: auto;
}

.add-btn {
  background: #f3f4f6;
  color: #6b7280;
}

.add-btn:hover {
  background: #e5e7eb;
  color: #374151;
}

.submit-btn {
  background: #6F00FF;
  color: white;
}

.submit-btn:hover {
  background: #5a00d4;
  transform: translateX(2px);
}

.suggestions {
  display: flex;
  gap: 1rem;
  justify-content: center;
  flex-wrap: wrap;
}

.suggestion-tag {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.75rem 1.25rem;
  background: white;
  border: 1px solid #e5e7eb;
  border-radius: 2rem;
  color: #374151;
  font-size: 0.9rem;
  cursor: pointer;
  transition: all 0.2s ease;
}

.suggestion-tag:hover {
  border-color: #6F00FF;
  color: #6F00FF;
  transform: translateY(-1px);
  box-shadow: 0 4px 12px rgba(111, 0, 255, 0.15);
}

.icon {
  font-size: 1rem;
}

/* 响应式设计 */
@media (max-width: 768px) {
  .main-content {
    padding: 1rem;
  }
  
  .main-title {
    font-size: 2rem;
  }
  
  .suggestions {
    flex-direction: column;
    align-items: center;
  }
  
  .suggestion-tag {
    width: 100%;
    max-width: 300px;
    justify-content: center;
  }
}
</style>
