<template>
  <div class="about-modal-overlay" v-click-outside.mousedown="closeModal" v-escape-key="closeModal"
    :class="{ 'animating': isAnimating }">
    <div class="about-modal" @click.stop :class="{ 'scale-in': isAnimating }">
      <div class="about-header">
        <div class="header-content">
          <div class="logo-section">
            <div class="about-logo"><img :src="logoUrl" alt="虚宁" /></div>

            <h2 class="about-title">关于光隅</h2>
          </div>
          <p class="version">v2.0.0</p>
        </div>
        <button class="close-btn" @click="closeModal">
          <SvgIcon name="close" />
        </button>
      </div>

      <div class="about-content">
        <div class="about-main">
          <div class="intro-section">
            <h3>在路上</h3>
            <blockquote>
            「 我便是世上的美好，永远闪耀 」
            </blockquote>
            <p>
            &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
            你好！屏幕前的你。此情此景，我们应该是初次相遇吧？但或许，我们应该是重逢的心情。谢谢你来这里看我，无论你是好奇还是对我有些关注。在这里，我留下了一些“关于我”的信息，希望你能在这里有些收获，也期待我和你能有更多共同的语言。<a style="color: var(--accent-color); font-weight: 500;text-shadow: 1px 1px 3px rgba(0,0,0,0.15);text-decoration: none;" href="https://www.bilibili.com/video/BV1Kj411g7Lu" target="_blank">「May you,the beauty of this world,always shine.」</a>
            </p>
          </div>
          <div class="hobby-section">
            <h3>爱好</h3>
            <p>
            健身 | Blender | 摄影 | 前端
            </p>
          </div>
          <div class="author-section">
            <h3>开发者</h3>
            <a href="https://github.com/jimmyshuixin" target="_blank" class="author-link">
              <div class="author-info">
                <img class="author-avatar" :src="ztmyoUrl" alt="虚宁">
                <div class="author-details">
                  <p class="author-name">@jimmyshuixin</p>
                  <p class="author-desc">全栈开发者</p>
                </div>
              </div>
            </a>
          </div>

          <div class="about-footer">
            <p>&copy; 2025 虚静以宁. Made with ❤️ by @jimmyshuixin</p>
            <p style="margin-top: 8px;">
              <a 
                href="https://beian.miit.gov.cn/" 
                target="_blank" 
                style="color: var(--text-color-tertiary); text-decoration: none;"
              >
                渝ICP备2025053763号-1
              </a>
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import SvgIcon from '@/components/SvgIcon.vue'
import { useScrollLock } from '@/composables/useScrollLock'

const emit = defineEmits(['close'])

const { lock, unlock } = useScrollLock()

// 静态资源URL
const logoUrl = new URL('@/assets/imgs/光隅.png', import.meta.url).href
const ztmyoUrl = new URL('@/assets/imgs/虚宁.png', import.meta.url).href

const isAnimating = ref(false)

const closeModal = () => {
  isAnimating.value = false
  unlock()
  setTimeout(() => {
    emit('close')
  }, 200)
}

onMounted(() => {
  lock()

  setTimeout(() => {
    isAnimating.value = true
  }, 10)
})
</script>

<style scoped>
.about-modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: var(--overlay-bg);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 2000;
  opacity: 0;
  transition: opacity 0.2s ease;
}

.about-modal-overlay.animating {
  opacity: 1;
}

.about-modal {
  background: var(--bg-color-primary);
  border-radius: 16px;
  width: 90%;
  max-width: 600px;
  max-height: 90vh;
  position: relative;
  transform: scale(0.9);
  transition: transform 0.2s ease;
  box-shadow: 0 20px 40px var(--shadow-color);
  display: flex;
  flex-direction: column;
  overflow: hidden;
  font-family: "Inter", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
}

.about-modal.scale-in {
  transform: scale(1);
}

.about-header {
  position: relative;
  background: var(--bg-color-primary);
  padding: 24px 32px;
  border-radius: 16px 16px 0 0;
  flex-shrink: 0;
}

.header-content {
  text-align: center;
}

.close-btn {
  position: absolute;
  top: 16px;
  right: 16px;
  width: 32px;
  height: 32px;
  border: none;
  background: var(--bg-color-secondary);
  color: var(--text-color-primary);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  z-index: 1;
  transition: all 0.2s ease;
}

.close-btn:hover {
  opacity: 0.8;
  transform: scale(1.1);
}

.about-content {
  flex: 1;
  overflow-y: auto;
  padding: 32px;
}

.logo-section {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 16px;
  margin-bottom: 12px;
}

.about-logo {
  width: 48px;
  height: 48px;
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: var(--primary-color);
}

.about-logo img {
  width: 120%;
  height: 100%;
  object-fit: contain;
}

.about-title {
  font-size: 28px;
  font-weight: 700;
  color: var(--text-color-primary);
  margin: 0;
}

.version {
  font-size: 14px;
  color: var(--text-color-secondary);
  background: var(--bg-color-secondary);
  padding: 4px 12px;
  border-radius: 12px;
  display: inline-block;
  margin: 0;
}

.about-main {
  display: flex;
  flex-direction: column;
  gap: 28px;
}

.intro-section h3,
.author-section h3,
.hobby-section h3 {
  font-size: 18px;
  font-weight: 600;
  color: var(--text-color-primary);
  margin: 0 0 12px 0;
}

.intro-section p,
.hobby-section p {
  font-size: 15px;
  line-height: 1.6;
  color: var(--text-color-secondary);
  margin: 0;
}

.intro-section blockquote {
    border-left: none;
    padding-left: 0;
    margin: 1rem 0;
    font-size: 1.1rem;
    color: var(--text-color-primary);
    font-weight: 600;
    font-style: normal;
}

.author-link {
  text-decoration: none;
  color: inherit;
  display: block;
  border-radius: 12px;
  padding: 12px;
  transition: all 0.3s ease;
}

.author-link:hover {
  background-color: var(--bg-color-secondary);
}

.author-info {
  display: flex;
  align-items: center;
  gap: 16px;
}

.author-avatar {
  width: 48px;
  height: 48px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  border: 1px solid var(--border-color-primary);
}



.author-details {
  flex: 1;
}

.author-name {
  font-size: 16px;
  font-weight: 600;
  color: var(--text-color-primary);
  margin: 0 0 4px 0;
}

.author-desc {
  font-size: 14px;
  color: var(--text-color-secondary);
  margin: 0;
}

.about-footer {
  text-align: center;
  margin-top: 32px;
  padding-top: 24px;
}

.about-footer p {
  font-size: 13px;
  color: var(--text-color-tertiary);
  margin: 0;
}

/* 移动端适配 - 全屏显示 */
@media (max-width: 768px) {
  .about-modal {
    width: 100vw;
    height: 100vh;
    max-width: 100vw;
    max-height: 100vh;
    border-radius: 0;
    transform: scale(1);
  }

  .about-modal.scale-in {
    transform: scale(1);
  }

  .close-btn {
    position: fixed;
    top: 40px;
    left: 16px;
    z-index: 2001;
    background: transparent;
    color: var(--text-color-secondary);
    width: 36px;
    height: 36px;
  }

  .close-btn:hover {
    background: rgba(144, 144, 144, 0.292);
    transform: scale(1);
  }

  .about-header {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    z-index: 2000;
    height: calc(72px + constant(safe-area-inset-top));
    height: calc(72px + env(safe-area-inset-top));
    padding: 12px 16px;
    padding-left: 60px;
    background: var(--bg-color-primary);
    border-bottom: 1px solid var(--border-color-primary);
    border-radius: 0;
  }

  .about-content {
    flex: 1;
    overflow-y: auto;
    overflow-x: hidden;
    padding-top: calc(100px + constant(safe-area-inset-top));
    padding-top: calc(100px + env(safe-area-inset-top));
    padding-bottom: calc(32px + constant(safe-area-inset-bottom));
    padding-bottom: calc(32px + env(safe-area-inset-bottom));
    padding-left: 16px;
    padding-right: 16px;
    max-width: 100vw;
    box-sizing: border-box;
    -webkit-overflow-scrolling: touch;
    touch-action: auto;
    overscroll-behavior: contain;
  }

  .logo-section {
    flex-direction: row;
    padding-top: 12px;
    gap: 12px;
    margin-bottom: -4px;
  }

  .about-title {
    font-size: 24px;
  }

  .contact-links {
    justify-content: center;
  }
}
</style>