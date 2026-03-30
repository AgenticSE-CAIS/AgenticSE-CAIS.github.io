<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const activeSection = ref('home')
const navCollapsed = ref(true)

const sections = [
  { id: 'home', label: 'Home' },
  { id: 'overview', label: 'Overview' },
  { id: 'submission', label: 'Call for Papers' },
  { id: 'dates', label: 'Dates' },
  { id: 'organizers', label: 'Organizers' },
]

const topics = [
  { title: 'Empirical Studies', desc: 'Analysis of agent behavior from real-world deployments, e.g., leveraging the AIDev dataset.' },
  { title: 'Architectures for Agentic Coding', desc: 'Composition strategies, tool use, memory management, and multi-agent coordination patterns.' },
  { title: 'Evaluation and Testing', desc: 'Moving beyond static code snippets to evaluate agents on repository-level tasks, fault localization, and regression testing.' },
  { title: 'Production Operations', desc: 'Monitoring, debugging, and maintaining agentic systems (MLOps, LLMOps, AgentOps) in production environments.' },
  { title: 'Human-Agent Collaboration', desc: 'Cognitive load, trust calibration, and the dynamics of AI-augmented developer workflows.' },
  { title: 'Safety and Integrity', desc: 'Supply chain security, prevention of hallucinated dependencies, and risk assessment in agent-generated code.' },
]

const dates = [
  { date: 'April 12, 2026', event: 'Workshop Paper Submission' },
  { date: 'May 5, 2026', event: 'Workshop Paper Notification' },
  { date: 'May 26, 2026', event: 'Workshop @ CAIS 2026, San Jose, CA' },
]

const organizers = [
  { name: 'Hao Li', website: 'https://leo-lihao.github.io', photo: '/images/haoli.jpg', affiliation: "Queen's University"},
  { name: 'Jie M. Zhang', website: 'https://sites.google.com/view/jie-zhang', photo: '/images/jiezhang.jpg', affiliation: "King's College London", objectPosition: '50% 10%'},
  { name: 'Chao Peng', website: 'https://chao-peng.github.io/', photo: '/images/peng_chao.jpg', affiliation: 'ByteDance' },
  { name: 'Shweta Garg', website: 'https://shwetagarg-dev.github.io/', photo: '/images/shweta_garg.jpg', affiliation: 'Amazon' },
  { name: 'Lingming Zhang', website: 'https://lingming.cs.illinois.edu/', photo: '/images/lingming_zhang.jpeg', affiliation: 'UIUC', objectPosition: '50% 0%'},
  { name: 'Qinghua Lu', website: 'https://people.csiro.au/L/Q/Qinghua-Lu', photo: '/images/qinghua_lu.jpg', affiliation: 'Data61, CSIRO' , objectPosition: '50% 10%'},
  { name: 'Satish Chandra', website: 'https://sites.google.com/site/schandraacmorg/', photo: '/images/satish_chandra.jpg', affiliation: 'Meta Platforms, Inc.' },
  { name: 'Thomas Zimmermann', website: 'https://thomas-zimmermann.com/', photo: '/images/thomaszimmermann.jpg', affiliation: 'UC Irvine' },
  { name: 'Ahmed E. Hassan', website: 'https://research.cs.queensu.ca/home/ahmed/home/', photo: '/images/ahmedhassan.jpg', affiliation: "Queen's University" },
]

function scrollTo(id) {
  navCollapsed.value = true
  const el = document.getElementById(id)
  if (el) el.scrollIntoView({ behavior: 'smooth' })
}

function handleScroll() {
  const scrollY = window.scrollY + 100
  for (let i = sections.length - 1; i >= 0; i--) {
    const el = document.getElementById(sections[i].id)
    if (el && el.offsetTop <= scrollY) {
      activeSection.value = sections[i].id
      break
    }
  }
}

onMounted(() => window.addEventListener('scroll', handleScroll))
onUnmounted(() => window.removeEventListener('scroll', handleScroll))
</script>

<template>
  <!-- Navbar -->
  <nav class="navbar navbar-expand-lg fixed-top">
    <div class="container-fluid px-4">
      <a class="navbar-brand" href="#" @click.prevent="scrollTo('home')">
        Agentic SE @ CAIS'26
      </a>
      <button
        class="navbar-toggler border-0"
        type="button"
        @click="navCollapsed = !navCollapsed"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" :class="{ show: !navCollapsed }">
        <ul class="navbar-nav ms-auto">
          <li class="nav-item" v-for="s in sections" :key="s.id">
            <a
              class="nav-link"
              :class="{ active: activeSection === s.id }"
              href="#"
              @click.prevent="scrollTo(s.id)"
            >{{ s.label }}</a>
          </li>
        </ul>
      </div>
    </div>
  </nav>

  <!-- Hero Text -->
  <section id="home" class="hero-text-section">
    <div class="container">
      <div class="row">
        <div class="col-lg-11">
          <span class="hero-badge">CAIS 2026 Workshop</span>
          <h1 class="hero-title">
            Agentic Software Engineering
          </h1>
          <p class="hero-subtitle">Software as the Frontier of Agentic Systems</p>
          <div class="hero-meta d-flex flex-wrap gap-4 mb-4">
            <div><i class="bi bi-calendar-event"></i> May 26, 2026</div>
            <div><i class="bi bi-geo-alt"></i> San Jose, California</div>
            <div><i class="bi bi-clock"></i> Full-Day</div>
          </div>
          <p class="mt-4" style="max-width: 800px; font-size: 1.15rem; line-height: 1.7;">
            Co-located with the <strong><a href="https://www.caisconf.org/" target="_blank" rel="noopener noreferrer" style="color: var(--primary); text-decoration: underline; text-underline-offset: 4px;">1st ACM Conference on AI and Agentic Systems (CAIS 2026)</a></strong>.
            Bridging AI and Software Engineering for reliable agentic systems.
          </p>
          <a href="https://www.caisconf.org/" target="_blank" rel="noopener" class="btn-register">
            Register at CAIS 2026 <i class="bi bi-arrow-right ms-2"></i>
          </a>
        </div>
      </div>
    </div>
  </section>

  <!-- Overview -->
  <section id="overview" class="section section-alt">
    <div class="container">
      <div class="row">
        <div class="col-lg-4">
          <h2 class="section-title">Workshop<br>Overview</h2>
        </div>
        <div class="col-lg-8">
          <hr class="section-divider d-lg-none">
          <p class="lead mb-4 text-dark" style="font-size: 1.25rem;">
            Agentic Software Engineering marks a fundamental shift from human-centric development to agentic systems that actively participate across the entire software lifecycle. Software engineering has emerged as a key frontier for such agentic systems. Agentic coding systems, such as Claude Code, OpenAI Codex, and GitHub Copilot, are among the first truly autonomous agents deployed in complex, real-world environments. 
            
            However, agentic systems are still software systems. Advancing this field requires deep collaboration between research communities. This workshop creates a collaborative venue to bridge these communities.
          </p>
        </div>
      </div>
    </div>
  </section>

  <!-- Submission / CTA -->
  <section id="submission" class="section">
    <div class="container">
      <div class="row">
        <div class="col-lg-4">
          <h2 class="section-title">Call for<br>Papers</h2>
        </div>
        <div class="col-lg-8">
          <hr class="section-divider d-lg-none">
          <p class="mb-5" style="font-size: 1.1rem; line-height: 1.8;">
            We invite submissions of original research papers, position papers, and demo papers
            on the following topics of interest. Papers should follow the ACM format.
            All accepted papers will be presented at the workshop.
          </p>
          
          <h4 class="fw-bold mb-4 text-uppercase" style="letter-spacing: 0.05em;">Topics of Interest</h4>
          <ul class="mb-5" style="font-size: 1.1rem; line-height: 1.8; color: var(--text-muted); list-style-type: disc; padding-left: 1.5rem;">
            <li v-for="t in topics" :key="t.title" class="mb-2">
              <strong style="color: var(--primary);">{{ t.title }}:</strong> {{ t.desc }}
            </li>
          </ul>

          <h4 class="fw-bold mb-4 text-uppercase" style="letter-spacing: 0.05em;">Submission Guidelines</h4>
          <ul class="mb-4" style="font-size: 1.1rem; line-height: 1.8; color: var(--text-muted);">
            <li><strong>Full papers:</strong> up to 4 pages (excluding references)</li>
            <li><strong>Extended abstracts:</strong> up to 2 pages for position papers, reports, and preliminary results</li>
            <li><strong>Format:</strong> ACM <span style="color: #e83e8c;">sigconf</span> double-column format — <a href="https://www.acm.org/publications/proceedings-template" target="_blank" rel="noopener noreferrer" style="color: var(--primary); font-weight: 600;">Download templates</a></li>
          </ul>
          
          <div class="mt-5 p-4 bg-white border" style="border-color: var(--border-color) !important;">
            <p class="mb-0 fw-bold text-uppercase" style="letter-spacing: 0.05em;">Submission portal coming soon</p>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- Important Dates -->
  <section id="dates" class="section section-alt">
    <div class="container">
      <div class="row">
        <div class="col-lg-4">
          <h2 class="section-title">Important<br>Dates</h2>
        </div>
        <div class="col-lg-8">
          <hr class="section-divider d-lg-none">
          <div class="date-list">
            <div class="date-item" v-for="d in dates" :key="d.date">
              <span class="date-badge">{{ d.date }}</span>
              <span class="date-event">{{ d.event }}</span>
            </div>
          </div>
          <p class="text-muted mt-4" style="font-size: 0.95rem;">
            <i class="bi bi-info-circle me-2"></i>
            All deadlines are at 11:59 PM AoE (Anywhere on Earth).
          </p>
        </div>
      </div>
    </div>
  </section>

  <!-- Organizers -->
  <section id="organizers" class="section">
    <div class="container">
      <div class="row mb-5">
        <div class="col-12">
          <h2 class="section-title text-center">Organizing Committee</h2>
        </div>
      </div>
      <div class="row g-4 justify-content-center row-cols-1 row-cols-sm-2 row-cols-lg-5">
        <div class="col" v-for="o in organizers" :key="o.name">
          <a v-if="o.website" :href="o.website" target="_blank" rel="noopener noreferrer" class="text-decoration-none" style="display: block; color: inherit; height: 100%;">
            <div class="organizer-card h-100">
              <img v-if="o.photo" class="avatar" :src="o.photo" :alt="o.name" :style="o.objectPosition ? { objectPosition: o.objectPosition } : {}">
              <div v-else class="avatar d-flex align-items-center justify-content-center bg-light text-muted" style="font-size: 3rem;">
                <i class="bi bi-person-fill"></i>
              </div>
              <h5 style="font-size: 1.05rem" class="mb-2">
                {{ o.name }}
              </h5>
              <p class="affiliation">{{ o.affiliation }}</p>
            </div>
          </a>
          <div v-else class="organizer-card h-100">
            <img v-if="o.photo" class="avatar" :src="o.photo" :alt="o.name" :style="o.objectPosition ? { objectPosition: o.objectPosition } : {}">
            <div v-else class="avatar d-flex align-items-center justify-content-center bg-light text-muted" style="font-size: 3rem;">
              <i class="bi bi-person-fill"></i>
            </div>
            <h5 style="font-size: 1.05rem" class="mb-2">{{ o.name }}</h5>
            <p class="affiliation">{{ o.affiliation }}</p>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- Footer -->
  <footer class="site-footer">
    <div class="container text-center">
      <h3 class="mb-4 fw-bold text-uppercase" style="letter-spacing: 0.05em;">Agentic Software Engineering</h3>
      <p class="mb-2" style="font-size: 1.1rem;">
        CAIS 2026 Workshop &middot; San Jose, California &middot; May 26, 2026
      </p>
      <p class="mb-5 mt-4" style="font-size: 1rem;">
        <strong>Contact us:</strong> <a href="mailto:hao.li@queensu.ca">hao.li@queensu.ca</a>
      </p>
      <p class="mb-0" style="font-size: 0.9rem; opacity: 0.7;">
        &copy; 2026 Agentic SE Workshop. Co-located with <a href="https://www.caisconf.org/" target="_blank" rel="noopener noreferrer">CAIS 2026</a>.
      </p>
    </div>
  </footer>
</template>
