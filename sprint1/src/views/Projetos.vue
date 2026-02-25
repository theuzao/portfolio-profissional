<template>
  <div class="projects-page">

    <div class="page-header container">
      <span class="page-badge mono">PG 02</span>
      <h1 class="page-title">Projetos</h1>
      <p class="page-subtitle">Lorem ipsum dolor sit amet, consectetur adipiscing elit.</p>
    </div>

    <div class="projects-layout">

      <aside class="sidebar">
        <div class="sidebar-label mono">Filtrar por</div>
        <button
          v-for="cat in categories"
          :key="cat"
          class="sidebar-item mono"
          :class="{ active: activeCategory === cat }"
          @click="activeCategory = cat"
        >
          {{ cat }}
        </button>
      </aside>

      <div class="timeline-area">
        <div class="timeline-line"></div>

        <TransitionGroup name="tl" tag="div" class="timeline-items">
          <div
            v-for="project in filteredProjects"
            :key="project.id"
            class="tl-item"
          >
            <div class="tl-year mono">{{ project.year }}</div>
            <div class="tl-dot" :class="{ active: project.live }"></div>
            <div class="tl-card" :class="{ featured: project.live }">
              <div class="tl-card-img">
                <span class="img-placeholder-text mono">🖼️ Screenshot / GIF do projeto</span>
                <span v-if="project.live" class="status-badge mono">● Live</span>
              </div>
              <div class="tl-card-body">
                <h3 class="tl-card-title">{{ project.name }}</h3>
                <p class="tl-card-desc">{{ project.description }}</p>
                <div class="tech-badges">
                  <span
                    v-for="tech in project.techs"
                    :key="tech"
                    class="tech-badge mono"
                  >{{ tech }}</span>
                </div>
                <a :href="project.github" target="_blank" rel="noopener" class="gh-link mono">
                  ⎋ Ver no GitHub ↗
                </a>
              </div>
            </div>
          </div>
        </TransitionGroup>

        <div v-if="filteredProjects.length === 0" class="empty-state mono">
          Nenhum projeto nesta categoria ainda.
        </div>
      </div>

    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const categories = ['Todos', 'Web App', 'Mobile', 'API / Back-end', 'Open Source', 'UI / Design']
const activeCategory = ref('Todos')

const projects = [
  {
    id: 1,
    year: '2023',
    name: 'Projeto 01',
    description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.',
    techs: ['HTML', 'CSS', 'JavaScript'],
    github: 'https://github.com/',
    category: 'Web App',
    live: false,
  },
  {
    id: 2,
    year: '2024',
    name: 'Projeto 02',
    description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.',
    techs: ['Vue.js', 'Node.js', 'PostgreSQL'],
    github: 'https://github.com/',
    category: 'Web App',
    live: false,
  },
  {
    id: 3,
    year: '2025',
    name: 'Portfólio Profissional',
    description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.',
    techs: ['Vue.js', 'Vite', 'Vue Router', 'CSS3'],
    github: 'https://github.com/',
    category: 'Web App',
    live: true,
  },
]

const filteredProjects = computed(() => {
  if (activeCategory.value === 'Todos') return projects
  return projects.filter((p) => p.category === activeCategory.value)
})
</script>

<style scoped>
.projects-page {
  min-height: calc(100vh - 64px - 62px);
  padding-bottom: 64px;
}

.page-header {
  padding: 52px 32px 32px;
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

.page-title {
  font-size: clamp(26px, 4vw, 42px);
  margin-bottom: 8px;
}

.page-subtitle {
  font-size: 14px;
  color: var(--text-secondary);
}

.projects-layout {
  display: grid;
  grid-template-columns: 200px 1fr;
  border-top: 1px solid var(--border);
  min-height: 400px;
}

.sidebar {
  border-right: 1px solid var(--border);
  padding: 24px 20px;
  display: flex;
  flex-direction: column;
  gap: 6px;
}

.sidebar-label {
  font-size: 9px;
  color: var(--text-muted);
  letter-spacing: 0.2em;
  text-transform: uppercase;
  margin-bottom: 8px;
}

.sidebar-item {
  padding: 8px 12px;
  border-radius: 6px;
  font-size: 11px;
  color: var(--text-secondary);
  border: 1px solid transparent;
  text-align: left;
  cursor: pointer;
  transition: all 0.18s;
  background: none;
}

.sidebar-item:hover {
  color: var(--text);
  background: var(--surface);
  border-color: var(--border);
}

.sidebar-item.active {
  background: var(--accent-dim);
  border-color: rgba(200, 245, 74, 0.3);
  color: var(--accent);
}

.timeline-area {
  padding: 32px;
  position: relative;
}

.timeline-line {
  position: absolute;
  left: 100px;
  top: 32px;
  bottom: 32px;
  width: 2px;
  background: linear-gradient(to bottom, var(--accent), var(--border));
  border-radius: 2px;
}

.timeline-items {
  display: flex;
  flex-direction: column;
  gap: 32px;
}

.tl-item {
  display: flex;
  gap: 22px;
  align-items: flex-start;
  position: relative;
}

.tl-year {
  width: 44px;
  font-size: 10px;
  color: var(--text-muted);
  text-align: right;
  padding-top: 7px;
  flex-shrink: 0;
}

.tl-dot {
  width: 12px;
  height: 12px;
  border-radius: 50%;
  background: var(--placeholder-light);
  border: 2px solid var(--surface-dark);
  flex-shrink: 0;
  margin-top: 5px;
  transition: background 0.2s, box-shadow 0.2s;
}

.tl-dot.active {
  background: var(--accent);
  box-shadow: 0 0 0 3px var(--accent-dim);
}

.tl-card {
  flex: 1;
  background: var(--surface-alt);
  border: 1px solid var(--border-light);
  border-radius: var(--radius-card);
  overflow: hidden;
  max-width: 580px;
  transition: border-color 0.2s, transform 0.2s;
  box-shadow: var(--shadow-main);
}

.tl-card:hover {
  border-color: rgba(200, 245, 74, 0.2);
  transform: translateY(-2px);
}

.tl-card.featured {
  border-color: rgba(200, 245, 74, 0.3);
}

.tl-card-img {
  height: 110px;
  background: var(--placeholder);
  border-bottom: 1px solid var(--border);
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
}

.img-placeholder-text {
  font-size: 11px;
  color: var(--text-muted);
}

.status-badge {
  position: absolute;
  top: 10px;
  right: 10px;
  background: rgba(0, 200, 80, 0.15);
  border: 1px solid rgba(0, 200, 80, 0.4);
  color: var(--green);
  font-size: 9px;
  padding: 3px 10px;
  border-radius: var(--radius-pill);
}

.tl-card-body {
  padding: 16px 20px 20px;
}

.tl-card-title {
  font-size: 15px;
  font-weight: 800;
  margin-bottom: 6px;
  color: var(--text);
}

.tl-card-desc {
  font-size: 13px;
  color: var(--text-secondary);
  line-height: 1.65;
  margin-bottom: 12px;
}

.tech-badges {
  display: flex;
  gap: 6px;
  flex-wrap: wrap;
  margin-bottom: 14px;
}

.tech-badge {
  height: 22px;
  padding: 0 9px;
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: var(--radius-badge);
  font-size: 10px;
  color: var(--text-muted);
  display: inline-flex;
  align-items: center;
}

.gh-link {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  font-size: 11px;
  color: var(--blue);
  border: 1px solid rgba(74, 144, 245, 0.3);
  border-radius: var(--radius-badge);
  padding: 5px 12px;
  background: rgba(74, 144, 245, 0.06);
  transition: background 0.18s;
}
.gh-link:hover {
  background: rgba(74, 144, 245, 0.14);
}

.empty-state {
  padding: 48px;
  text-align: center;
  color: var(--text-muted);
  font-size: 13px;
}

.tl-enter-active,
.tl-leave-active {
  transition: opacity 0.25s ease, transform 0.25s ease;
}
.tl-enter-from {
  opacity: 0;
  transform: translateX(8px);
}
.tl-leave-to {
  opacity: 0;
  transform: translateX(-8px);
}

@media (max-width: 900px) {
  .timeline-line {
    left: 76px;
  }
}

@media (max-width: 768px) {
  .projects-layout {
    grid-template-columns: 1fr;
  }
  .sidebar {
    border-right: none;
    border-bottom: 1px solid var(--border);
    flex-direction: row;
    flex-wrap: wrap;
    padding: 16px;
    gap: 8px;
  }
  .sidebar-label {
    width: 100%;
    margin-bottom: 0;
  }
  .timeline-line {
    left: 80px;
  }
}

@media (max-width: 480px) {
  .timeline-area {
    padding: 24px 16px;
  }
  .timeline-line {
    left: 64px;
  }
  .tl-card {
    max-width: 100%;
  }
}
</style>
