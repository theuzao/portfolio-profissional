<template>
  <div class="contact-page">

    <div class="page-header container">
      <span class="page-badge mono">PG 04</span>
      <h1 class="page-title">Contato</h1>
      <p class="page-subtitle">Lorem ipsum dolor sit amet, consectetur adipiscing elit.</p>
    </div>

    <div class="contact-layout container">

      <div class="contact-left">
        <p class="section-label mono">Redes sociais</p>
        <div class="social-grid">
          <a
            v-for="social in socials"
            :key="social.name"
            :href="social.url"
            target="_blank"
            rel="noopener"
            class="social-card"
          >
            <div class="social-icon">{{ social.icon }}</div>
            <div class="social-info">
              <span class="social-name mono">{{ social.name }}</span>
              <span class="social-handle mono">{{ social.handle }}</span>
            </div>
          </a>
        </div>
      </div>

      <div class="contact-right">
        <p class="form-label mono">Enviar mensagem</p>

        <form @submit.prevent="handleSubmit" class="contact-form" novalidate>

          <div class="form-field">
            <label class="field-label mono" for="name">Nome</label>
            <input
              id="name"
              v-model="form.name"
              type="text"
              placeholder="Seu nome completo"
              required
              autocomplete="name"
            />
          </div>

          <div class="form-field">
            <label class="field-label mono" for="email">E-mail</label>
            <input
              id="email"
              v-model="form.email"
              type="email"
              placeholder="seu@email.com"
              required
              autocomplete="email"
            />
          </div>

          <div class="form-field">
            <label class="field-label mono" for="message">Mensagem</label>
            <textarea
              id="message"
              v-model="form.message"
              rows="5"
              placeholder="Escreva sua mensagem..."
              required
            ></textarea>
          </div>

          <button type="submit" class="submit-btn mono" :disabled="sending">
            {{ sending ? 'Enviando...' : 'Enviar mensagem →' }}
          </button>

          <Transition name="fade">
            <p
              v-if="feedback"
              class="feedback mono"
              :class="feedback.type"
            >{{ feedback.text }}</p>
          </Transition>

        </form>
      </div>

    </div>
  </div>
</template>

<script setup>
import { ref, reactive } from 'vue'

const socials = [
  { name: 'GitHub',   icon: '🐙', handle: '@seu-usuario',       url: 'https://github.com/' },
  { name: 'LinkedIn', icon: '💼', handle: 'in/matheus-pereira', url: 'https://linkedin.com/in/' },
  { name: 'E-mail',   icon: '📧', handle: 'matheus@email.com',  url: 'mailto:matheus@email.com' },
  { name: 'WhatsApp', icon: '💬', handle: '+55 (31) 9xxxx-xxxx', url: 'https://wa.me/' },
]

const form = reactive({ name: '', email: '', message: '' })
const sending = ref(false)
const feedback = ref(null)

async function handleSubmit() {
  sending.value = true
  feedback.value = null

  await new Promise((r) => setTimeout(r, 900))

  sending.value = false
  feedback.value = {
    type: 'success',
    text: '✓ Mensagem enviada! Em breve retornarei o contato.',
  }
  form.name = ''
  form.email = ''
  form.message = ''

  setTimeout(() => { feedback.value = null }, 6000)
}
</script>

<style scoped>
.contact-page {
  min-height: calc(100vh - 64px - 62px);
  padding-bottom: 64px;
}

.page-header {
  padding: 52px 32px 40px;
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

.contact-layout {
  display: grid;
  grid-template-columns: 1fr 400px;
  gap: 64px;
  align-items: start;
}

.section-label {
  font-size: 10px;
  color: var(--text-muted);
  letter-spacing: 0.15em;
  text-transform: uppercase;
  margin-bottom: 16px;
}

.social-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 12px;
}

.social-card {
  display: flex;
  align-items: center;
  gap: 14px;
  padding: 16px 18px;
  border: 1px solid var(--border-light);
  border-radius: var(--radius-card);
  background: var(--surface-alt);
  text-decoration: none;
  transition: border-color 0.2s, background 0.2s, transform 0.15s;
}

.social-card:hover {
  border-color: rgba(200, 245, 74, 0.25);
  background: var(--accent-dim2);
  transform: translateY(-2px);
}

.social-icon {
  width: 42px;
  height: 42px;
  border-radius: 8px;
  background: var(--placeholder);
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 20px;
  flex-shrink: 0;
}

.social-info {
  display: flex;
  flex-direction: column;
  gap: 4px;
  min-width: 0;
}

.social-name {
  font-size: 13px;
  color: var(--text);
  font-weight: 700;
}

.social-handle {
  font-size: 10px;
  color: var(--text-muted);
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.form-label {
  font-size: 10px;
  color: var(--text-secondary);
  letter-spacing: 0.15em;
  text-transform: uppercase;
  margin-bottom: 20px;
}

.contact-form {
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.form-field {
  display: flex;
  flex-direction: column;
  gap: 7px;
}

.field-label {
  font-size: 11px;
  color: var(--text-secondary);
  letter-spacing: 0.06em;
}

input,
textarea {
  background: #1c1c1c;
  border: 1px solid var(--border-light);
  border-radius: 8px;
  padding: 10px 14px;
  color: var(--text);
  font-family: 'Syne', sans-serif;
  font-size: 14px;
  outline: none;
  transition: border-color 0.2s, box-shadow 0.2s;
  resize: vertical;
}

input:focus,
textarea:focus {
  border-color: var(--accent);
  box-shadow: 0 0 0 2px var(--accent-dim);
}

input::placeholder,
textarea::placeholder {
  color: var(--text-muted);
  font-size: 13px;
}

.submit-btn {
  height: 46px;
  background: var(--accent);
  color: #000;
  font-size: 12px;
  font-weight: 700;
  letter-spacing: 0.15em;
  text-transform: uppercase;
  border-radius: 8px;
  cursor: pointer;
  border: none;
  opacity: 0.82;
  transition: opacity 0.2s, transform 0.15s;
}

.submit-btn:hover:not(:disabled) {
  opacity: 1;
  transform: translateY(-1px);
}

.submit-btn:disabled {
  opacity: 0.45;
  cursor: not-allowed;
}

.feedback {
  font-size: 12px;
  padding: 10px 14px;
  border-radius: 6px;
}

.feedback.success {
  background: rgba(0, 200, 80, 0.1);
  border: 1px solid rgba(0, 200, 80, 0.3);
  color: var(--green);
}

.feedback.error {
  background: rgba(255, 80, 80, 0.1);
  border: 1px solid rgba(255, 80, 80, 0.3);
  color: #ff6060;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

@media (max-width: 900px) {
  .contact-layout {
    grid-template-columns: 1fr;
    gap: 40px;
  }
}

@media (max-width: 480px) {
  .social-grid {
    grid-template-columns: 1fr;
  }
}
</style>
