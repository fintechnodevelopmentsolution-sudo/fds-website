<script setup>
import { onMounted, ref } from 'vue'

const isLoading = ref(true)
const isMenuOpen = ref(false)
const submitted = ref(false)
const form = ref({ name: '', email: '', service: '' })
const services = [
  { number: '01', title: 'Custom Website Company Profile', text: 'Website informatif, berkarakter, dan mudah ditemukan.', tag: 'STRATEGI + DEV', image: 'https://images.unsplash.com/photo-1558655146-d09347e92766?auto=format&fit=crop&w=1000&q=85' },
  { number: '02', title: 'Custom Website Professional', text: 'Pengalaman digital premium untuk mengubah pengunjung menjadi pelanggan.', tag: 'DESIGN + DEV', image: 'https://images.unsplash.com/photo-1460925895917-afdab827c52f?auto=format&fit=crop&w=1000&q=85' },
  { number: '03', title: 'Custom Website Undangan Online', text: 'Undangan digital yang personal, praktis, dan memorable.', tag: 'PERSONAL PROJECT', image: 'https://images.unsplash.com/photo-1519225421980-715cb0215aed?auto=format&fit=crop&w=1000&q=85' },
]
const steps = [
  ['01', 'Dengar & pahami', 'Kami mulai dari konteks, bukan asumsi.'],
  ['02', 'Rancang dengan niat', 'Setiap detail punya alasan dan tujuan.'],
  ['03', 'Bangun & bertumbuh', 'Hasil yang siap diluncurkan dan dikembangkan.'],
]
function scrollTo(id) { isMenuOpen.value = false; document.getElementById(id)?.scrollIntoView({ behavior: 'smooth' }) }
function submitForm() { submitted.value = true }
onMounted(() => window.setTimeout(() => { isLoading.value = false }, 700))
</script>

<template>
  <div class="site-shell">
    <Transition name="loader">
      <div v-if="isLoading" class="page-loader"><div class="loader-brand"><span class="brand-mark">F</span><strong>FINTECHNO</strong></div><div class="loader-line"><span></span></div><p>LOADING EXPERIENCE</p></div>
    </Transition>
    <header class="topbar">
      <a class="brand" href="#top" @click.prevent="scrollTo('top')"><span class="brand-mark">F</span><span>FINTECHNO<span class="brand-muted">/FDS</span></span></a>
      <button class="menu-toggle" :aria-expanded="isMenuOpen" aria-label="Buka navigasi" @click="isMenuOpen = !isMenuOpen"><span></span><span></span></button>
      <nav class="nav-links" :class="{ open: isMenuOpen }"><a href="#services" @click.prevent="scrollTo('services')">Layanan</a><a href="#process" @click.prevent="scrollTo('process')">Cara kerja</a><a href="#contact" @click.prevent="scrollTo('contact')">Kontak</a><button class="nav-cta" @click="scrollTo('contact')">Mulai proyek <span>↗</span></button></nav>
    </header>

    <main id="top">
      <section class="hero section-pad"><div class="hero-copy"><p class="eyebrow"><span class="pulse-dot"></span> Digital partner for ambitious ideas</p><h1>MAKE IT<br /><em>MATTER.</em></h1><p class="hero-intro">Kami membantu bisnis dan personal brand hadir lebih kuat di dunia digital — dari ide pertama sampai siap diluncurkan.</p><button class="text-button" @click="scrollTo('services')">Lihat layanan <span>↓</span></button></div><div class="hero-visual" aria-label="Ilustrasi abstrak teknologi"><div class="visual-grid"></div><div class="orbit orbit-one"></div><div class="orbit orbit-two"></div><div class="visual-core"><span>FDS</span><small>EST. 2020</small></div><div class="visual-label label-top">IDEA<br /><strong>→</strong></div><div class="visual-label label-bottom">DESIGN<br /><strong>→</strong></div></div><div class="hero-footnote">SCROLL TO EXPLORE <span>↓</span></div></section>
      <section class="marquee"><div class="marquee-track"><span>WEB DEVELOPMENT</span><b>✳</b><span>VISUAL IDENTITY</span><b>✳</b><span>UI/UX DESIGN</span><b>✳</b><span>WEB DEVELOPMENT</span></div></section>
      <section id="services" class="services section-pad"><div class="section-heading"><p class="eyebrow">01 / Apa yang kami kerjakan</p><h2>Built for your<br /><em>next move.</em></h2><p class="heading-note">Solusi digital yang dirancang untuk membuat brand kamu terlihat, terasa, dan diingat.</p></div><div class="service-cards"><article v-for="service in services" :key="service.number" class="service-card"><div class="card-image"><img :src="service.image" :alt="service.title" loading="lazy" /><span class="service-number">{{ service.number }}</span><span class="card-arrow">↗</span></div><div class="card-content"><span class="service-tag">{{ service.tag }}</span><h3>{{ service.title }}</h3><p>{{ service.text }}</p><button class="card-link" @click="scrollTo('contact')">Bahas project <span>↗</span></button></div></article></div></section>
      <section id="process" class="process section-pad"><div class="process-intro"><p class="eyebrow">02 / Cara kami bekerja</p><h2>Good work<br /><em>feels clear.</em></h2></div><div class="steps"><div v-for="step in steps" :key="step[0]" class="step"><span class="step-number">{{ step[0] }}</span><div><h3>{{ step[1] }}</h3><p>{{ step[2] }}</p></div></div></div></section>
      <section id="contact" class="contact section-pad"><div class="contact-heading"><p class="eyebrow">03 / Mari ngobrol</p><h2>Punya ide?<br /><em>Let's make it real.</em></h2></div><form class="contact-form" @submit.prevent="submitForm"><template v-if="!submitted"><label>Nama kamu<input v-model="form.name" required type="text" placeholder="Nama lengkap" /></label><label>Email aktif<input v-model="form.email" required type="email" placeholder="nama@email.com" /></label><label>Yang ingin dibuat<select v-model="form.service" required><option disabled value="">Pilih layanan</option><option>Website Company Profile</option><option>Website Professional</option><option>Undangan Online</option><option>Desain Grafis & UI/UX</option></select></label><button class="submit-button" type="submit">Kirim brief <span>↗</span></button></template><div v-else class="success-state"><span class="success-icon">✓</span><h3>Brief terkirim.</h3><p>Terima kasih, {{ form.name }}. Tim kami akan menghubungi kamu segera.</p></div></form></section>
    </main>
    <footer class="footer section-pad"><div><a class="brand" href="#top"><span class="brand-mark">F</span><span>FINTECHNO<span class="brand-muted">/FDS</span></span></a><p>Technology with a point of view.</p></div><div class="footer-meta"><span>YOGYAKARTA · INDONESIA</span><span>© 2024 FDS</span><a href="mailto:hello@fintechno.id">hello@fintechno.id ↗</a></div></footer>
  </div>
</template>
