<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const activeSection = ref('home')
const navCollapsed = ref(true)

const sections = [
  { id: 'home', label: 'Home' },
  { id: 'overview', label: 'Overview' },
  { id: 'submission', label: 'Call for Papers' },
  { id: 'dates', label: 'Dates' },
  { id: 'travel', label: 'Travel Support' },
  { id: 'organizers', label: 'Organizers' },
  { id: 'pc', label: 'Program Committee' },
]

const topics = [
  { title: 'Empirical Studies', desc: 'Analysis of agent behavior from real-world deployments, e.g., leveraging the <a href="https://huggingface.co/datasets/hao-li/AIDev" target="_blank" rel="noopener noreferrer" style="color: var(--primary); font-weight: 600;">AIDev</a> dataset.' },
  { title: 'Architectures for Agentic Coding', desc: 'Composition strategies, tool use, memory management, and multi-agent coordination patterns.' },
  { title: 'Evaluation and Testing', desc: 'Moving beyond static code snippets to evaluate agents on repository-level tasks, fault localization, and regression testing.' },
  { title: 'Production Operations', desc: 'Monitoring, debugging, and maintaining agentic systems (MLOps, LLMOps, AgentOps) in production environments.' },
  { title: 'Human-Agent Collaboration', desc: 'Cognitive load, trust calibration, and the dynamics of AI-augmented developer workflows.' },
  { title: 'Safety and Integrity', desc: 'Supply chain security, prevention of hallucinated dependencies, and risk assessment in agent-generated code.' },
]

const dates = [
  { date: 'May 1, 2026', event: 'Workshop Poster Submission' },
  { date: '<del>April 20</del>, <del>April 25</del>, April 28, 2026', event: 'Workshop Paper Submission' },
  { date: 'May 5, 2026', event: 'Accept/Reject Notification' },
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

const pc = [
  { name: 'Saima Afrin', title: 'PhD Student', affiliation: 'College of William and Mary' },
  { name: 'Joseph Axisa', title: 'Software Engineer', affiliation: 'Google' },
  { name: 'Hema Sekhar Reddy Busireddy', title: 'Researcher', affiliation: 'Google' },
  { name: 'Advitya Gemawat', title: 'Researcher', affiliation: 'Microsoft' },
  { name: 'Jiayi Geng', title: 'PhD Student', affiliation: 'Carnegie Mellon University' },
  { name: 'Anwar Ghammam', title: 'Assistant Professor', affiliation: 'University of Michigan-Dearborn' },
  { name: 'Nishant Gupta', title: 'Researcher', affiliation: 'Meta' },
  { name: 'Yinglong Li', title: 'Software Engineer', affiliation: 'Google' },
  { name: 'Yu Shi', title: 'PhD Student', affiliation: "Queen's University", role: 'Web Chair' },
  { name: 'Lintang Sutawika', title: 'PhD Student', affiliation: 'Carnegie Mellon University' },
  { name: 'Zehao Wang', title: 'PhD Student', affiliation: 'Concordia University' },
  { name: 'Haoxiang Zhang', title: 'Adjunct Research Associate', affiliation: "Queen's University" },
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
          <p class="hero-subtitle">The Frontier of Agentic Systems</p>
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
            
            However, agentic systems are still software systems. Advancing this field requires deep collaboration between the artificial intelligence and software engineering research communities. This workshop creates a collaborative venue to bridge these two communities.
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
            The main event will feature invited talks and panel discussions. We offer two submission tracks covering our topics of interest:
            <br>
            • <strong>Poster Track:</strong> A broader showcase welcoming all forms of work, including arXiv preprints, recently accepted papers, and relevant past work.<br>
            • <strong>Paper Track:</strong> For new, original research (long, short, or position papers).
          </p>
          
          <h4 class="fw-bold mb-4 text-uppercase" style="letter-spacing: 0.05em;">Topics of Interest</h4>
          <ul class="mb-5" style="font-size: 1.1rem; line-height: 1.8; color: var(--text-muted); list-style-type: disc; padding-left: 1.5rem;">
            <li v-for="t in topics" :key="t.title" class="mb-2">
              <strong style="color: var(--primary);">{{ t.title }}:</strong> <span v-html="t.desc"></span>
            </li>
          </ul>

          <h4 class="fw-bold mb-4 text-uppercase" style="letter-spacing: 0.05em;">Poster Submission</h4>
          <ul class="mb-4" style="font-size: 1.1rem; line-height: 1.8; color: var(--text-muted);">
            <li><strong>Format:</strong> a short abstract (max 2,000 characters) and a PDF copy of your poster (max 10 MB).</li>
            <li><strong>Review:</strong> Submissions will be evaluated for relevance to the workshop topics and potential to generate discussion.</li>
            <li><strong>Early Notification:</strong> <span style="color: var(--primary); font-weight: 600;">Please submit when ready! We will review and notify you as soon as possible.</span></li>
          </ul>

          <div class="mb-5">
            <a href="https://docs.google.com/forms/d/e/1FAIpQLSfCdXUMfjh8lGvOWVheOV-onnj9n-pyJp97sCUEa6mF4nGT1A/viewform?usp=dialog" target="_blank" rel="noopener noreferrer" class="btn-register">
              Submit Poster (Google Form) <i class="bi bi-arrow-right ms-2"></i>
            </a>
            <p class="mt-2 text-muted" style="font-size: 0.95rem;">
              <i class="bi bi-info-circle me-1"></i> Authors can keep the form response link to continue updating their submission until the deadline.
            </p>
          </div>

          <h4 class="fw-bold mb-4 text-uppercase" style="letter-spacing: 0.05em;">Paper Submission</h4>
          <ul class="mb-4" style="font-size: 1.1rem; line-height: 1.8; color: var(--text-muted);">
            <li><strong>Long papers:</strong> Up to 8 pages (excluding references).</li>
            <li><strong>Short/Position papers:</strong> Up to 4 pages (excluding references).</li>
            <li><strong>Format:</strong> ACM double-column format <a href="https://www.acm.org/publications/proceedings-template" target="_blank" rel="noopener noreferrer" style="color: var(--primary); font-weight: 600;">(download template)</a>. Use <code style="background: #f1f5f9; padding: 0.15rem 0.4rem; font-size: 0.9rem;">\documentclass[sigconf,anonymous,review]{acmart}</code></li>
            <li><strong>Review:</strong> All submissions are double-blind. Please anonymize your submission.</li>
            <li><strong>Proceedings:</strong> The workshop is a non-archival showcase venue. There will be no formal proceedings.</li>
          </ul>
          
          <div>
            <a href="https://openreview.net/group?id=ACM.org/CAIS/2026/Workshop/AgenticSE" target="_blank" rel="noopener noreferrer" class="btn-register">
              Submit Paper (OpenReview) <i class="bi bi-arrow-right ms-2"></i>
            </a>
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
            <div class="date-item" v-for="d in dates" :key="d.event">
              <span class="date-badge" v-html="d.date"></span>
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

  <!-- Travel Support -->
  <section id="travel" class="section">
    <div class="container">
      <div class="row">
        <div class="col-lg-4">
          <h2 class="section-title">Travel<br>Support</h2>
        </div>
        <div class="col-lg-8">
          <hr class="section-divider d-lg-none">

          <div class="mb-5">
            <h4 class="fw-bold mb-2" style="letter-spacing: 0.05em;">SIGSOFT Travel Support for the AgenticSE Workshop</h4>
            <p class="mb-4 text-muted">
              <strong>Deadline:</strong> before April 27, 2026 | <a href="https://docs.google.com/forms/d/e/1FAIpQLSf-afN-DnpfnwESH6su0PuYPLmcAsskPyRCNW2acI2jWOnL6w/viewform?usp=dialog" target="_blank" rel="noopener noreferrer" style="color: var(--primary); font-weight: 600; text-decoration: underline; text-underline-offset: 4px;">Application Form</a>
            </p>

            <p class="mb-4" style="font-size: 1.1rem; line-height: 1.8;">
              SIGSOFT is pleased to offer travel support for students and professionals who attend the AgenticSE workshop. This travel support can be used for reimbursing flight, hotel, taxi/cab, shuttle, meals, mileage, and parking, and shall NOT be used for reimbursing other expenses (in particular, conference registration). The support is available for anyone who fits into one or more of the following categories:
            </p>

            <ul class="mb-4" style="font-size: 1.1rem; line-height: 1.8; list-style-type: disc; padding-left: 1.5rem;">
              <li>participants who identify as being a member of an underrepresented racial or ethnic group(s) in the place they work,</li>
              <li>participants based in low income and lower middle income countries as identified by the World Bank List of Economies,</li>
              <li>undergraduate students, or</li>
              <li><a href="https://www.acm.org/special-interest-groups/sigs/sigsoft" target="_blank" rel="noopener noreferrer" style="color: var(--primary); text-decoration: underline; text-underline-offset: 4px;">SIGSOFT</a> members (both student and professional, yearly fee is $20).</li>
            </ul>

            <p class="mb-4" style="font-size: 1.1rem; line-height: 1.8;">
              The support is limited. To apply, please complete the <a href="https://docs.google.com/forms/d/e/1FAIpQLSf-afN-DnpfnwESH6su0PuYPLmcAsskPyRCNW2acI2jWOnL6w/viewform?usp=dialog" target="_blank" rel="noopener noreferrer" style="color: var(--primary); text-decoration: underline; text-underline-offset: 4px;">application form</a> before April 27. The notifications will be sent by May 1.
            </p>
            
            <p class="mb-4" style="font-size: 1.1rem; line-height: 1.8;">
              Due to the limited budget and oftentimes a large number of qualified applicants, we can provide only partial support for attendance.
            </p>

            <p class="mb-0" style="font-size: 1.1rem; line-height: 1.8;">
              Please do not apply multiple times. Only one application will be considered. You will receive an email confirmation that allows you to update your application.
            </p>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- Organizers -->
  <section id="organizers" class="section section-alt">
    <div class="container">
      <div class="row mb-5">
        <div class="col-12">
          <h2 class="section-title text-center">Organizing Committee</h2>
        </div>
      </div>
      <div class="row g-4 justify-content-center row-cols-1 row-cols-sm-2 row-cols-lg-5">
        <div class="col" v-for="o in organizers" :key="o.name">
          <component 
            :is="o.website ? 'a' : 'div'"
            v-bind="o.website ? { href: o.website, target: '_blank', rel: 'noopener noreferrer' } : {}"
            :class="o.website ? 'text-decoration-none' : ''"
            :style="[o.website ? { display: 'block', color: 'inherit' } : {}, { height: '100%' }]"
          >
            <div class="organizer-card h-100">
              <img v-if="o.photo" class="avatar" :src="o.photo" :alt="o.name" :style="o.objectPosition ? { objectPosition: o.objectPosition } : {}">
              <div v-else class="avatar d-flex align-items-center justify-content-center bg-light text-muted" style="font-size: 3rem;">
                <i class="bi bi-person-fill"></i>
              </div>
              <h5 style="font-size: 1.05rem" class="mb-2">{{ o.name }}</h5>
              <p class="affiliation">{{ o.affiliation }}</p>
            </div>
          </component>
        </div>
      </div>
    </div>
  </section>

  <!-- Program Committee -->
  <section id="pc" class="section">
    <div class="container">
      <div class="row mb-5">
        <div class="col-12">
          <h2 class="section-title text-center">Program Committee</h2>
        </div>
      </div>
      <div class="row justify-content-center">
        <div class="col-lg-8">
          <ul class="pc-list">
            <li v-for="p in pc" :key="p.name" class="pc-item">
              <strong>{{ p.name }}</strong><span v-if="p.role" class="text-muted"> ({{ p.role }})</span>
              <span class="text-muted"> — {{ p.title }}, {{ p.affiliation }}</span>
            </li>
          </ul>
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
