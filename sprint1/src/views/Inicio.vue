<template>
  <div class="home">

    <section class="hero">
      <div class="container hero-inner">

        <div class="hero-left">
          <h1 class="hero-title">
            Matheus <span class="accent">Pereira</span>
          </h1>

          <p class="hero-subtitle">
            Lorem ipsum dolor sit amet, consectetur adipiscing elit.
          </p>

          <div class="hero-btns">
            <RouterLink to="/projetos" class="btn-primary mono">Ver Projetos ↓</RouterLink>
            <a href="#" class="btn-secondary mono">Download CV ↗</a>
          </div>
        </div>

        <div class="hero-right">
          <div class="avatar-placeholder">
            <span class="avatar-icon">🖼️</span>
          </div>
        </div>

      </div>
    </section>

    <section class="about">
      <div class="about-grid">
        <div class="about-lang">
          <span class="lang-tag mono">🇧🇷 Português</span>
          <p>
            Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor
            incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud
            exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat duis aute irure
            dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
          </p>
        </div>
        <div class="about-lang">
          <span class="lang-tag mono">🇺🇸 English</span>
          <p>
            Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor
            incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud
            exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat duis aute irure
            dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
          </p>
        </div>
      </div>
    </section>

    <section class="skills">
      <div class="container skills-strip">
        <span class="skills-label mono">Stack →</span>
        <span v-for="skill in skills" :key="skill" class="skill-badge mono">{{ skill }}</span>
      </div>
    </section>

  </div>
</template>

<script setup>
import { RouterLink } from 'vue-router'

const skills = [
  'Java', 'Spring Boot', 'Python', 'TypeScript',
  'Vue.js', 'Node.js', 'PostgreSQL', 'Docker', 'Git',
]
</script>

<style scoped>
.hero {
  padding: 72px 0 56px;
}

.hero-inner {
  display: grid;
  grid-template-columns: 1fr 300px;
  gap: 64px;
  align-items: center;
}

.hero-left {
  display: flex;
  flex-direction: column;
  gap: 24px;
}

.hero-title {
  font-size: clamp(38px, 5vw, 64px);
  line-height: 1.05;
  color: var(--text);
}

.hero-subtitle {
  font-size: 15px;
  color: var(--text-secondary);
  line-height: 1.7;
}

.hero-btns {
  display: flex;
  gap: 12px;
  flex-wrap: wrap;
}

.btn-primary {
  display: inline-flex;
  align-items: center;
  padding: 11px 26px;
  background: var(--accent);
  color: #000;
  font-size: 11px;
  font-weight: 700;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  border-radius: 8px;
  text-decoration: none;
  opacity: 0.82;
  transition: opacity 0.2s, transform 0.15s;
}
.btn-primary:hover {
  opacity: 1;
  transform: translateY(-1px);
}

.btn-secondary {
  display: inline-flex;
  align-items: center;
  padding: 11px 26px;
  border: 1px solid var(--border-light);
  color: var(--text-secondary);
  font-size: 11px;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  border-radius: 8px;
  text-decoration: none;
  transition: border-color 0.2s, color 0.2s;
}
.btn-secondary:hover {
  border-color: var(--accent);
  color: var(--accent);
}

.hero-right {
  display: flex;
  justify-content: center;
}

.avatar-placeholder {
  width: 220px;
  height: 260px;
  background: var(--placeholder);
  border: 1px solid var(--border-light);
  border-radius: 16px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 10px;
  position: relative;
  overflow: hidden;
}

.avatar-placeholder::before {
  content: '';
  position: absolute;
  inset: 0;
  background: linear-gradient(135deg, var(--accent-dim2) 0%, transparent 60%);
}

.avatar-icon {
  font-size: 36px;
  position: relative;
}


.about {
  border-top: 1px solid var(--border);
}

.about-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
}

.about-lang {
  background: var(--surface-dark);
  padding: 40px;
  border-right: 1px solid var(--border);
  display: flex;
  flex-direction: column;
  gap: 16px;
  position: relative;
  overflow: hidden;
}

.about-lang:last-child {
  border-right: none;
}

.about-lang::before {
  content: '';
  position: absolute;
  left: 0;
  top: 0;
  bottom: 0;
  width: 3px;
  background: linear-gradient(to bottom, var(--accent), transparent);
}

.lang-tag {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  font-size: 10px;
  color: var(--text-secondary);
  background: var(--surface);
  border: 1px solid var(--border);
  padding: 4px 12px;
  border-radius: var(--radius-badge);
  width: fit-content;
}

.about-lang p {
  font-size: 14px;
  color: var(--text-secondary);
  line-height: 1.8;
}

.skills {
  border-top: 1px solid var(--border);
  padding: 20px 0;
}

.skills-strip {
  display: flex;
  align-items: center;
  gap: 10px;
  flex-wrap: wrap;
}

.skills-label {
  font-size: 10px;
  color: var(--text-muted);
  letter-spacing: 0.18em;
  text-transform: uppercase;
  margin-right: 4px;
}

.skill-badge {
  height: 30px;
  padding: 0 14px;
  border: 1px solid var(--border-light);
  border-radius: var(--radius-pill);
  background: var(--surface);
  display: inline-flex;
  align-items: center;
  font-size: 11px;
  color: var(--text-secondary);
  transition: border-color 0.2s, color 0.2s;
  cursor: default;
}
.skill-badge:hover {
  border-color: var(--accent);
  color: var(--accent);
}

@media (max-width: 768px) {
  .hero-inner {
    grid-template-columns: 1fr;
    gap: 40px;
  }
  .hero-right {
    order: -1;
  }
  .about-grid {
    grid-template-columns: 1fr;
  }
  .about-lang {
    border-right: none;
    border-bottom: 1px solid var(--border);
    padding: 28px 24px;
  }
  .about-lang:last-child {
    border-bottom: none;
  }
}

@media (max-width: 480px) {
  .hero {
    padding: 40px 0 36px;
  }
  .avatar-placeholder {
    width: 160px;
    height: 190px;
  }
}
</style>
