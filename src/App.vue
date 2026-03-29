<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const activeSection = ref('home')
const navCollapsed = ref(true)

const sections = [
  { id: 'home', label: 'Home' },
  { id: 'submission', label: 'Call for Papers' },
  { id: 'dates', label: 'Important Dates' },
  { id: 'program', label: 'Program' },
  { id: 'organizers', label: 'Organizers' },
]

const topics = [
  { icon: 'bi-bar-chart-line', title: 'Empirical Studies', desc: 'Analysis of agent behavior from real-world deployments, e.g., leveraging the AIDev dataset.' },
  { icon: 'bi-boxes', title: 'Architectures for Agentic Coding', desc: 'Composition strategies, tool use, memory management, and multi-agent coordination patterns.' },
  { icon: 'bi-check2-all', title: 'Evaluation and Testing', desc: 'Moving beyond static code snippets to evaluate agents on repository-level tasks, fault localization, and regression testing.' },
  { icon: 'bi-gear-wide-connected', title: 'Production Operations', desc: 'Monitoring, debugging, and maintaining agentic systems (MLOps, LLMOps, AgentOps) in production environments.' },
  { icon: 'bi-people', title: 'Human-Agent Collaboration', desc: 'Cognitive load, trust calibration, and the dynamics of AI-augmented developer workflows.' },
  { icon: 'bi-shield-check', title: 'Safety and Integrity', desc: 'Supply chain security, prevention of hallucinated dependencies, and risk assessment in agent-generated code.' },
]

const dates = [
  { date: 'March 24, 2026', event: 'Workshop Website and CFP' },
  { date: 'April 12, 2026', event: 'Workshop Paper Submission' },
  { date: 'May 5, 2026', event: 'Workshop Paper Notification' },
  { date: 'May 26, 2026', event: 'Workshop @ CAIS 2026, San Jose, CA' },
]

const organizers = [
  { name: 'Hao Li', website: 'https://leo-lihao.github.io', photo: '/images/haoli.jpg', affiliation: "Queen's University", role: '', bio: "Postdoctoral Fellow at Queen's University. Co-Chair of the MSR 2026 Mining Challenge. Research focuses on agentic workflows at the intersection of Software Engineering and AI." },
  { name: 'Jie M. Zhang', website: 'https://sites.google.com/view/jie-zhang', photo: '/images/jiezhang.jpg', affiliation: "King's College London", role: '', bio: "Lecturer at King's College London and visiting AI scientist at Mistral AI. Research focuses on AI and software trustworthiness." },
  { name: 'Chao Peng', website: 'https://chao-peng.github.io/', photo: '/images/peng_chao.jpg', affiliation: 'ByteDance', role: '', bio: 'Principal Research Scientist at ByteDance, leading the Software Engineering Lab on AI agents for software engineering.' },
  { name: 'Shweta Garg', website: 'https://shwetagarg-dev.github.io/', photo: '/images/shweta_garg.jpg', affiliation: 'Amazon', role: '', bio: 'AI Research Lead driving applied research in code intelligence and interactive agents for developer productivity.' },
  { name: 'Lingming Zhang', website: 'https://lingming.cs.illinois.edu/', photo: '/images/lingming_zhang.jpeg', affiliation: 'UIUC', role: '', bio: 'Associate Professor at UIUC. His group has pioneered work on LLM-based software testing, analysis, repair, and synthesis.' },
  { name: 'Qinghua Lu', website: 'https://people.csiro.au/L/Q/Qinghua-Lu', photo: '/images/qinghua_lu.jpg', affiliation: 'Data61, CSIRO', role: '', bio: 'Acting Research Director of Software and Computational Systems Research Program at CSIRO, specialising in AI engineering and responsible AI.' },
  { name: 'Satish Chandra', website: 'https://sites.google.com/site/schandraacmorg/', photo: '/images/satish_chandra.jpg', affiliation: 'Meta Platforms, Inc.', role: '', bio: 'Research scientist at Meta, applying machine learning techniques to improve developer productivity.' },
  { name: 'Thomas Zimmermann', website: 'https://thomas-zimmermann.com/', photo: '/images/thomaszimmermann.jpg', affiliation: 'UC Irvine', role: '', bio: "Chancellor's Professor and Bren Chair at UC Irvine. Research at the intersection of software engineering, machine learning, AI, and data science." },
  { name: 'Ahmed E. Hassan', website: 'https://research.cs.queensu.ca/home/ahmed/home/', photo: '/images/ahmedhassan.jpg', affiliation: "Queen's University", role: '', bio: "Mustafa Prize Laureate, Fellow of ACM, IEEE, and AAIA. Canada Research Chair in Software Engineering." },
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
  <nav class="navbar navbar-expand-lg navbar-dark fixed-top">
    <div class="container">
      <a class="navbar-brand fw-bold" href="#" @click.prevent="scrollTo('home')">
        <i class="bi bi-robot me-2"></i>Agentic SE @ CAIS'26
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
  <section id="home" class="hero-text-section pt-5 mt-5 pb-4">
    <div class="container position-relative" style="z-index: 1;">
      <div class="row">
        <div class="col-lg-10">
          <span class="hero-badge">CAIS 2026 Workshop</span>
          <h1 class="hero-title">
            Agentic Software Engineering
            
          </h1>
          <p class="hero-subtitle">Software as the Frontier of Agentic Systems</p>
          <p class="hero-meta mb-2">
            <i class="bi bi-calendar-event"></i> May 26, 2026
            <span class="mx-2">|</span>
            <i class="bi bi-geo-alt"></i> San Jose, California
            <span class="mx-2">|</span>
            <i class="bi bi-clock"></i> Full-Day
          </p>
          <p class="hero-meta" style="max-width: 800px; margin-top: 1.5rem; font-size: 1.05rem; line-height: 1.7;">
            Co-located with the <a href="https://www.caisconf.org/" target="_blank" rel="noopener noreferrer" style="color: inherit; text-decoration: underline;">1st ACM Conference on AI and Agentic Systems (CAIS 2026)</a>.
            Bridging AI and Software Engineering for reliable agentic systems.
          </p>
          <a href="https://www.caisconf.org/" target="_blank" rel="noopener" class="btn-register">
            <i class="bi bi-box-arrow-up-right"></i> Register at CAIS 2026
          </a>
        </div>
      </div>
    </div>
  </section>



  <!-- Overview -->
  <section class="section">
    <div class="container">
      <h2 class="section-title">Workshop Overview</h2>
      <hr class="section-divider">
      <div class="row">
        <div class="col-lg-10">
          <p class="lead" style="font-size: 1.05rem;">
            Agentic Software Engineering marks a fundamental shift from human-centric development to agentic systems that actively participate across the entire software lifecycle. Agentic systems are no longer theoretical; they are deployed at scale, generating millions of pull requests on GitHub and fundamentally changing how software is built.
          </p>
          <p style="font-size: 1.02rem; color: var(--text-muted);">
            However, agentic systems are still software systems. Advancing this field requires deep collaboration between research communities. The AI community drives foundational breakthroughs in compound AI architectures, sophisticated reasoning paradigms, multi-agent orchestration, and long-horizon planning, while the software engineering community provides the complex evaluation environments, production operations expertise, and the empirical rigor required for deployment. This workshop creates a collaborative venue at CAIS 2026 to bridge these disciplines. We aim to establish a cross-community research agenda that is both architecturally advanced and empirically grounded.
          </p>
        </div>
      </div>
    </div>
  </section>

  <!-- Submission / CTA -->
  <section id="submission" class="section section-alt">
    <div class="container">
      <h2 class="section-title">Call for Papers</h2>
      <hr class="section-divider">
      <div>
        <div class="row align-items-center">
          <div class="col-lg-8">
            <p style="opacity: 0.9; font-size: 0.98rem; line-height: 1.8;">
              We invite submissions of original research papers, position papers, and demo papers
              on the following topics of interest. Papers should follow the ACM format.
              All accepted papers will be presented at the workshop.
            </p>
            <h5 class="fw-bold mt-4 mb-2">Topics of Interest:</h5>
            <ul style="opacity: 0.85; font-size: 0.92rem;" class="mb-4">
              <li v-for="t in topics" :key="t.title" class="mb-1">
                <strong>{{ t.title }}</strong>: {{ t.desc }}
              </li>
            </ul>
            <h5 class="fw-bold mt-4 mb-2">Submission Guidelines:</h5>
            <ul style="opacity: 0.85; font-size: 0.92rem;" class="mb-3">
              <li>Full papers: up to 4 pages (excluding references)</li>
              <li>Extended abstracts: up to 2 pages for position papers, reports, and preliminary results</li>
              <li>Format: <a href="https://www.caisconf.org/call-for-papers" target="_blank" rel="noopener noreferrer" style="color: inherit; text-decoration: underline;">ACM double-column</a></li>
            </ul>
          </div>
          <div class="col-lg-4 text-lg-end mt-3 mt-lg-0">
            <p class="mb-2" style="opacity: 0.7; font-size: 0.85rem;">Submission portal coming soon</p>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- Important Dates -->
  <section id="dates" class="section">
    <div class="container">
      <h2 class="section-title">Important Dates</h2>
      <hr class="section-divider">
      <div class="col-lg-8">
        <div class="date-item" v-for="d in dates" :key="d.date">
          <span class="date-badge">{{ d.date }}</span>
          <span style="font-size: 1.02rem;">{{ d.event }}</span>
        </div>
        <p class="text-muted mt-3" style="font-size: 0.88rem;">
          <i class="bi bi-info-circle me-1"></i>
          All deadlines are at 11:59 PM AoE (Anywhere on Earth).
        </p>
      </div>
    </div>
  </section>

  <!-- Program Sketch -->
  <section id="program" class="section section-alt">
    <div class="container">
      <h2 class="section-title">Program Sketch</h2>
      <hr class="section-divider">
      <p class="mb-4 text-muted">Full-day workshop featuring invited talks, paper presentations, and panel discussions.</p>
      <!-- <div class="col-lg-10">
        <table class="table program-table">
          <thead>
            <tr>
              <th style="width: 160px;">Time</th>
              <th>Event</th>
            </tr>
          </thead>
          <tbody>
            <tr><td>TBD</td><td>Opening Remarks</td></tr>
            <tr><td>TBD</td><td>Keynote Talk 1</td></tr>
            <tr><td>TBD</td><td>Paper Presentations — Session 1</td></tr>
            <tr><td>TBD</td><td>Coffee Break</td></tr>
            <tr><td>TBD</td><td>Keynote Talk 2</td></tr>
            <tr><td>TBD</td><td>Paper Presentations — Session 2</td></tr>
            <tr><td>TBD</td><td>Panel Discussion: The Future of AI Teammates</td></tr>
            <tr><td>TBD</td><td>Closing Remarks</td></tr>
          </tbody>
        </table>
      </div> -->
    </div>
  </section>

  <!-- Organizers -->
  <section id="organizers" class="section">
    <div class="container">
      <h2 class="section-title">Organizing Committee</h2>
      <hr class="section-divider">
      <div class="row g-4 justify-content-center">
        <div class="col-12 col-md-6 col-lg-4" v-for="o in organizers" :key="o.name">
          <div class="organizer-card">
            <img v-if="o.photo" class="avatar" :src="o.photo" :alt="o.name" :style="o.objectPosition ? { objectPosition: o.objectPosition } : {}">
            <div v-else class="avatar d-flex align-items-center justify-content-center bg-secondary text-white" style="font-size: 2rem;">
              <i class="bi bi-person-fill"></i>
            </div>
            <h5>
              <a v-if="o.website" :href="o.website" target="_blank" rel="noopener noreferrer" style="color: inherit; text-decoration: underline; text-underline-offset: 3px;">
                {{ o.name }}
              </a>
              <template v-else>{{ o.name }}</template>
            </h5>
            <p class="affiliation">{{ o.affiliation }}</p>
            <span v-if="o.role" class="role-badge">{{ o.role }}</span>
          </div>
        </div>
      </div>

    </div>
  </section>

  <!-- Footer -->
  <footer class="site-footer">
    <div class="container text-center">
      <p class="mb-1">
        <strong>Agentic Software Engineering</strong> — CAIS 2026 Workshop
      </p>
      <p class="mb-1">
        <i class="bi bi-geo-alt me-1"></i> San Jose, California &middot;
        <i class="bi bi-calendar3 ms-2 me-1"></i> May 26, 2026
      </p>
      <p class="mb-3 mt-3" style="font-size: 0.9rem;">
        <strong>Contact us:</strong> Please send questions and enquiries to <a href="mailto:hao.li@queensu.ca" style="color: inherit; text-decoration: underline;">hao.li@queensu.ca</a>
      </p>
      <p class="mb-0" style="font-size: 0.82rem; opacity: 0.6;">
        &copy; 2026 Agentic SE Workshop. Co-located with <a href="https://www.caisconf.org/" target="_blank" rel="noopener noreferrer" style="color: inherit; text-decoration: underline;">CAIS 2026</a>.
      </p>
    </div>
  </footer>
</template>
