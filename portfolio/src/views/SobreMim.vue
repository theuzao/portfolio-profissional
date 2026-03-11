<template>
  <div class="sobre-page">

    <div class="page-header container">
      <span class="page-badge mono">PG 01</span>
      <div class="header-row">
        <h1 class="page-title">{{ content[lang].title }}</h1>
        <div class="lang-toggle">
          <button
            class="lang-btn mono"
            :class="{ active: lang === 'pt' }"
            @click="lang = 'pt'"
          >🇧🇷 PT</button>
          <button
            class="lang-btn mono"
            :class="{ active: lang === 'en' }"
            @click="lang = 'en'"
          >🇺🇸 EN</button>
        </div>
      </div>
      <p class="page-subtitle">{{ content[lang].subtitle }}</p>
    </div>

    <div class="sobre-layout container">

      <div class="bio-section">
        <Transition name="fade" mode="out-in">
          <div :key="lang" class="bio-block">
            <div class="bio-card" v-for="(para, i) in content[lang].bio" :key="i">
              <p>{{ para }}</p>
            </div>
          </div>
        </Transition>

      </div>

      <aside class="sobre-aside">

        <div class="aside-block">
          <p class="aside-title mono">{{ content[lang].stackTitle }}</p>
          <div class="skill-list">
            <div
              v-for="skill in skills"
              :key="skill.name"
              class="skill-row"
            >
              <span class="skill-name mono">{{ skill.name }}</span>
              <div class="skill-bar">
                <div class="skill-fill" :style="{ width: skill.level + '%' }"></div>
              </div>
              <span class="skill-pct mono">{{ skill.level }}%</span>
            </div>
          </div>
        </div>


        <div class="aside-block">
          <p class="aside-title mono">{{ content[lang].educationTitle }}</p>
          <div class="edu-card" v-for="edu in content[lang].education" :key="edu.course">
            <span class="edu-icon">{{ edu.icon }}</span>
            <div>
              <p class="edu-course">{{ edu.course }}</p>
              <p class="edu-inst mono">{{ edu.institution }}</p>
              <p class="edu-period mono">{{ edu.period }}</p>
            </div>
          </div>
        </div>

      </aside>

    </div>

  </div>
</template>

<script setup>
import { ref } from 'vue'

const lang = ref('pt')

const content = {
  pt: {
    title: 'Sobre Mim',
    subtitle: 'Engenheiro de Software em formação. Construo sistemas desde os 13 anos, sem saber que isso tinha nome.',
    stackTitle: 'Stack principal',
    educationTitle: 'Formação',
    bio: [
      'Aos treze anos, tive meu primeiro contato com programação através do Habbo Hotel, onde atuei criando eventos, promoções e minigames utilizando HTML e CSS. Na época parecia apenas uma brincadeira, mas foi ali que comecei a desenvolver minhas primeiras habilidades técnicas.',
      'Anos depois, durante a pandemia, o contato com obras como Serial Experiments Lain despertou um interesse mais profundo sobre identidade digital e tecnologia. A partir disso, passei a estudar programação de forma intencional e decidi seguir carreira na área. Hoje curso Engenharia de Software na PUC Minas e busco desenvolver sistemas que tenham propósito e impacto real.',
      'Atualmente, minha principal linguagem é Java, e tenho direcionado meus estudos para a área de dados, explorando como transformar informação em sistemas mais inteligentes.',
    ],
    education: [
      {
        icon: '🎓',
        course: 'Engenharia de Software',
        institution: 'PUC Minas',
        period: '2024.2 – 2028.1 (previsão)',
      },
    ],
  },
  en: {
    title: 'About Me',
    subtitle: 'Software Engineering student. Building systems since age 13, before knowing it had a name.',
    stackTitle: 'Main Stack',
    educationTitle: 'Education',
    bio: [
      'At thirteen, I had my first contact with programming through Habbo Hotel, where I created events, promotions, and mini-games using HTML and CSS. At the time it felt like just a hobby, but that is where I began developing my first technical skills.',
      'Years later, during the pandemic, works like Serial Experiments Lain sparked a deeper interest in digital identity and technology. From that point on, I started studying programming with intention and decided to pursue a career in the field. Today I study Software Engineering at PUC Minas and aim to build systems with real purpose and impact.',
      'Currently, my main language is Java, and I have been directing my studies toward data, exploring how to turn information into smarter systems.',
    ],
    education: [
      {
        icon: '🎓',
        course: 'Software Engineering',
        institution: 'PUC Minas',
        period: '2024.2 – 2028.1 (expected)',
      },
    ],
  },
}

const skills = [
  { name: 'Java / Spring Boot', level: 75 },
  { name: 'JavaScript',         level: 70 },
  { name: 'Vue.js',             level: 70 },
  { name: 'React',              level: 65 },
  { name: 'Docker',             level: 60 },
  { name: 'PostgreSQL',         level: 60 },
]
</script>

<style scoped>
.sobre-page {
  min-height: calc(100vh - 64px - 62px);
  padding-bottom: 64px;
}

.page-header {
  padding: 52px 32px 36px;
}

.page-badge {
  font-size: 10px;
  letter-spacing: 0.2em;
  color: var(--accent);
  background: var(--accent-dim);
  border: 1px solid var(--accent);
  padding: 3px 10px;
  border-radius: var(--radius-badge);
  display: inline-block;
  margin-bottom: 14px;
}

.header-row {
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-wrap: wrap;
  gap: 16px;
  margin-bottom: 10px;
}

.page-title {
  font-size: clamp(26px, 4vw, 42px);
}

.page-subtitle {
  font-size: 14px;
  color: var(--text-secondary);
  max-width: 600px;
}

/* Language toggle */
.lang-toggle {
  display: flex;
  gap: 6px;
}

.lang-btn {
  padding: 6px 14px;
  border-radius: 6px;
  font-size: 11px;
  border: 1px solid var(--border);
  color: var(--text-secondary);
  cursor: pointer;
  background: none;
  transition: all 0.18s;
}
.lang-btn:hover {
  border-color: var(--border-light);
  color: var(--text);
}
.lang-btn.active {
  background: var(--accent-dim);
  border-color: rgba(200, 245, 74, 0.4);
  color: var(--accent);
}

/* Layout */
.sobre-layout {
  display: grid;
  grid-template-columns: 1fr 320px;
  gap: 48px;
  align-items: start;
}

/* Bio */
.bio-block {
  display: flex;
  flex-direction: column;
  gap: 14px;
}

.bio-card {
  padding: 20px 24px;
  background: var(--surface-alt);
  border: 1px solid var(--border-light);
  border-radius: var(--radius-card);
  border-left: 3px solid var(--accent);
}

.bio-card p {
  font-size: 14px;
  color: var(--text-secondary);
  line-height: 1.85;
}


/* Aside */
.sobre-aside {
  display: flex;
  flex-direction: column;
  gap: 24px;
}

.aside-block {
  background: var(--surface-alt);
  border: 1px solid var(--border-light);
  border-radius: var(--radius-card);
  padding: 20px;
}

.aside-title {
  font-size: 9px;
  color: var(--text-muted);
  letter-spacing: 0.2em;
  text-transform: uppercase;
  margin-bottom: 16px;
}

/* Skills */
.skill-list {
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.skill-row {
  display: grid;
  grid-template-columns: 140px 1fr 36px;
  align-items: center;
  gap: 10px;
}

.skill-name {
  font-size: 11px;
  color: var(--text-secondary);
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.skill-bar {
  height: 4px;
  background: var(--border);
  border-radius: 2px;
  overflow: hidden;
}

.skill-fill {
  height: 100%;
  background: var(--accent);
  border-radius: 2px;
  transition: width 0.6s cubic-bezier(0.4, 0, 0.2, 1);
}

.skill-pct {
  font-size: 10px;
  color: var(--text-muted);
  text-align: right;
}

/* Interests */
.interest-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
}

.interest-tag {
  font-size: 10px;
  padding: 4px 10px;
  border: 1px solid var(--border);
  border-radius: var(--radius-pill);
  color: var(--text-secondary);
  background: var(--surface);
  cursor: default;
  transition: border-color 0.18s, color 0.18s;
}
.interest-tag:hover {
  border-color: var(--accent);
  color: var(--accent);
}

/* Education */
.edu-card {
  display: flex;
  gap: 14px;
  align-items: flex-start;
}

.edu-icon {
  font-size: 22px;
  margin-top: 2px;
  flex-shrink: 0;
}

.edu-course {
  font-size: 13px;
  color: var(--text);
  font-weight: 700;
  margin-bottom: 2px;
}

.edu-inst {
  font-size: 11px;
  color: var(--text-secondary);
}

.edu-period {
  font-size: 10px;
  color: var(--text-muted);
  margin-top: 2px;
}

/* Transition */
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.22s ease, transform 0.22s ease;
}
.fade-enter-from {
  opacity: 0;
  transform: translateY(6px);
}
.fade-leave-to {
  opacity: 0;
  transform: translateY(-4px);
}

/* Responsive */
@media (max-width: 900px) {
  .sobre-layout {
    grid-template-columns: 1fr;
  }
}

@media (max-width: 600px) {
  .page-header {
    padding: 40px 20px 28px;
  }
  .skill-row {
    grid-template-columns: 120px 1fr 32px;
  }
  .highlights {
    gap: 20px;
  }
}

@media (max-width: 480px) {
  .header-row {
    flex-direction: column;
    align-items: flex-start;
  }
}
</style>
