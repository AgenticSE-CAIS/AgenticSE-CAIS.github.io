<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const activeSection = ref('home')
const navCollapsed = ref(true)

const sections = [
  { id: 'home', label: 'Home' },
  { id: 'program', label: 'Schedule' },
  { id: 'speakers', label: 'Speakers' },
  { id: 'submission', label: 'Call for Papers' },
  { id: 'dates', label: 'Dates' },
  { id: 'organizers', label: 'Committee' },
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
  { date: '<del>May 1, 2026</del>', event: '<del>Workshop Poster Submission</del>' },
  { date: '<del>April 20</del>, <del>April 25</del>, <del>April 28, 2026</del>', event: '<del>Workshop Paper Submission</del>' },
  { date: '<del>May 5, 2026</del>', event: '<del>Accept/Reject Notification</del>' },
  { date: 'May 26, 2026', event: 'Workshop @ CAIS 2026, San Jose, CA' },
]

const programSchedule = [
  { time: '08:30 - 08:40 am', title: 'Opening Remarks' },
  { time: '08:40 - 09:40 am', title: 'AI in SE: Google\'s DevAI Journey for Internal Developer Productivity', speaker: 'Niranjan Tulpule', affiliation: 'VP, Developer AI @ Google', speakerId: 'speaker-niranjan' },
  { time: '09:40 - 10:40 am', title: 'Poster Session & Coffee Break' },
  { time: '10:40 - 11:10 am', title: 'Inside The Agent Factory', speaker: 'Jonathan "Peli" de Halleux', affiliation: 'Microsoft Research & GitHub Next', speakerId: 'speaker-peli' },
  { time: '11:10 - 11:40 am', title: 'Two Futures of Programming', speaker: 'Graham Neubig', affiliation: 'Carnegie Mellon University & OpenHands', speakerId: 'speaker-neubig' },
  { time: '11:40 - 12:30 pm', title: 'Panel Discussion', speaker: 'Niranjan Tulpule, Jonathan "Peli" de Halleux, Graham Neubig' },
  { time: '12:30 - 1:30 pm', title: 'Lunch' },
  { time: '1:30 - 2:30 pm', title: 'In Code They Act, In Proof We Trust', speaker: 'Erik Meijer', affiliation: 'Leibniz Labs & Normal Computing', speakerId: 'speaker-erik' },
  { time: '2:30 - 3:00 pm', title: 'Building the Brain for Coding Agents', speaker: 'Behrooz Omidvar-Tehrani', affiliation: 'Science Lead @ AWS Agentic AI', speakerId: 'speaker-behrooz' },
  { time: '3:00 - 3:30 pm', title: 'Coffee Break' },
  { time: '3:30 - 4:00 pm', title: 'Codev: An Operating System for AI and Humans to Work Together', speaker: 'Waleed Kadous', affiliation: 'Founder @ Cluesmith', speakerId: 'speaker-waleed' },
  { time: '4:00 - 4:30 pm', title: 'Evaluating Agentic Software Engineering with Terminal-Bench, Harbor Adapters, and Harbor Index', speaker: 'Lin Shi', affiliation: 'Cornell Tech', speakerId: 'speaker-lin' },
  { time: '4:30 - 5:20 pm', title: 'Panel Discussion', speaker: 'Erik Meijer, Behrooz Omidvar-Tehrani, Waleed Kadous, Lin Shi' },
  { time: '5:20 - 5:30 pm', title: 'Closing Remarks' },
]

const speakers = [
  {
    id: 'speaker-niranjan',
    name: 'Niranjan Tulpule',
    affiliation: 'VP, Developer AI @ Google',
    website: 'https://www.linkedin.com/in/niranjantulpule/',
    photo: '/images/niranjan.jpeg',
    time: '08:40 - 09:40 am',
    title: 'AI in SE: Google\'s DevAI Journey for Internal Developer Productivity',
    abstract: '<p>In this talk, Niranjan will cover the journey of building AI capabilities across the Software Engineering Lifecycle, scaling adoption, and driving culture change across Google.</p><p>This talk will also cover how Google uses Antigravity internally across Google\'s internal monorepo and git ecosystems, and some of the agents deployed to take on autonomous, ambient tasks.</p><p>This journey required balancing rigorous SE standards and quality attributes while rapidly applying frontier GenAI innovations, designing new benchmarks and AI-native metrics, and changing developer infrastructure and tools from a purely assistive to an agentic approach.</p><p>Google\'s vast scale and diversity of ecosystems present a unique challenge, especially as the volume of code grows exponentially.</p>',
    bio: 'Niranjan Tulpule is the Vice President of Developer AI at Google, where he leads initiatives to fundamentally transform software creation and delivery across the company. With over 20 years of experience in developer tools, he brings deep domain expertise in applying artificial intelligence to software engineering. Niranjan has been a core part of Google\'s engineering organization since August 2005. Prior to his current role, he contributed to and led engineering efforts across several major product areas, including Core Developer, Google Cloud DevOps, Firebase, Google+, Gmail, Google Chrome, and Google Desktop.',
  },
  {
    id: 'speaker-peli',
    name: 'Jonathan "Peli" de Halleux',
    affiliation: 'Microsoft Research & GitHub Next',
    website: 'https://www.linkedin.com/in/pelidehalleux/',
    photo: '/images/peli.png',
    time: '10:40 - 11:10 am',
    title: 'Inside The Agent Factory',
    abstract: 'GitHub Agentic Workflows delivers safe and scalable repository automation on top of GitHub Actions and Copilot CLI. Most interestingly, Agentic Workflows is written almost exclusively by agents and used to automate its own software life cycle. In this talk, Peli de Halleux will share lessons learned while building software at scale with the help of 200 daily agents, helping through documentation, testing, specification enforcement or mining or even styling the output of the CLI. We will discuss processes that were discovered during this practice that hint at the future of software factories as Agentic Human Processes.',
    bio: 'Jonathan "Peli" de Halleux joined the Foundations for Software Engineering (new RiSE) in October 2006. Peli worked in the CLR as a SDET in charge of the Just In Time compiler (2004-2006). Before joining Microsoft, Peli earned a PhD in Applied Mathematics from the Catholic University of Louvain (2000-2004). During his time at RiSE, he built Pex (dynamic symbolic execution), MakeCode (K12 coding editors), GenAIScript (LLM scripting) and recently GitHub Agentic Workflows.',
  },
  {
    id: 'speaker-neubig',
    name: 'Graham Neubig',
    affiliation: 'Carnegie Mellon University & OpenHands',
    website: 'http://www.phontron.com/',
    photo: '/images/neubig_graham.png',
    time: '11:10 - 11:40 am',
    title: 'Two Futures of Programming',
    abstract: 'The agentic coding that has made shock waves across the software engineering world tends to be largely oriented around synchronous new feature development — a programmer works together with an agent and monitors its progress as the agent progresses. However, within software engineering, there are also many other tasks such as deployment, monitoring, maintenance, and upgrades which take as much or even more time. In this talk I will discuss about how the requirements for agents differ between the two varieties of tasks, and some research work that we are doing to make agents better for repetitive and mundane tasks, allowing programmers to focus on more creative work.',
    bio: 'Graham Neubig is an associate professor at the Language Technologies Institute of Carnegie Mellon University and Chief Scientist at OpenHands. His research focuses on large language models, including both fundamental advances in model capabilities and applications to tasks such as software development. His final goal is that every person in the world should be able to communicate with each-other, and with computers in their own language. He also contributes to making NLP research more accessible through open publishing of research papers, advanced NLP course materials and video lectures, and open-source software, all of which are available on his web site.',
  },
  {
    id: 'speaker-erik',
    name: 'Erik Meijer',
    affiliation: 'Leibniz Labs & Normal Computing',
    website: 'https://www.linkedin.com/in/erikmeijer1',
    photo: '/images/erik.jpg',
    time: '1:30 - 2:30 pm',
    title: 'In Code They Act, In Proof We Trust',
    abstract: '<p>AI agents today execute on blind trust, and the failure modes are already in the headlines: a dealership chatbot agreeing to sell a $76,000 Chevy Tahoe for $1, a coding agent wiping a production database during a code freeze, an "agent skill" quietly installing a keylogger on a developer\'s machine. These are not edge cases. They are the predictable consequence of allowing agents to act without any mechanical guarantee of correctness or safety.</p><p>Execution is irreversible. You cannot unsend a message, unwire a payment, or un-delete a database. In that regime, permitting an unsafe action costs far more than withholding a safe one, and thus the economically rational choice is to refuse to let agents act on unchecked intent alone.</p><p>Automind is an agent harness that enforces this discipline by construction. Before any action runs, the agent must submit its execution plan together with a machine-checkable proof of safety and correctness, written in Universalis, a literate logic programming language designed to be read by humans and verified by machines. A small, auditable checker decides whether the plan is allowed to execute.</p><p>By left-shifting the trust boundary, we no longer have to trust the agent\'s proposal, or even its proof; only the checker. Policy compliance becomes a static property, established before the first side effect. We can finally demand formal proofs, not vibes, from the agents we deploy.</p>',
    bio: 'Erik Meijer is an accomplished language, API, and type system designer who has worked on the design of Haskell, Mondrian, C#, Visual Basic, Dart, and Hack, and advised on the design of Java, Scala, JavaScript, and Kotlin. He is the original inventor of Rx (Reactive Extensions). At Microsoft, he led incubation around Cloud Programmability; at Facebook, he revamped the server-side programming stack and founded a team building reactive backend infrastructure for the social graph. He holds a honorary professorship in Programming Language Design at the University of Nottingham, has over 149 granted patents, and an h-index of 47.',
  },
  {
    id: 'speaker-behrooz',
    name: 'Behrooz Omidvar-Tehrani',
    affiliation: 'Science Lead @ AWS Agentic AI',
    website: 'https://www.linkedin.com/in/behroozomidvar',
    photo: '/images/behrooz.png',
    time: '2:30 - 3:00 pm',
    title: 'Building the Brain for Coding Agents',
    abstract: 'Coding agents already incorporate forms of memory, including project context, session histories, and user preferences. However, their memory architectures remain fragmented and insufficient for sustaining the continuity expected of a true programming partner. This talk examines what a principled memory system for coding agents entails. We discuss how distinct forms of remembering, from recalling past interactions to internalizing codebase structure to learning reusable strategies, contribute to the developer experience in fundamentally different ways. Drawing on concrete examples from production systems like Kiro and Claude Code, we identify where current designs succeed and where critical gaps persist, particularly around lifecycle governance, real-time retrieval, and long-term adaptation.',
    bio: 'Behrooz Omidvar-Tehrani is a Senior Applied Scientist and Science Lead at AWS Agentic AI, where he drives research on agentic code transformation and coding agents. Previously, he was a Research Scientist at LIG (Grenoble Informatics Laboratory) and NAVER LABS Europe, and a Postdoctoral Researcher at The Ohio State University. He holds a PhD in Mathematics and Computer Science from Université Grenoble Alpes.',
  },
  {
    id: 'speaker-waleed',
    name: 'Waleed Kadous',
    affiliation: 'Founder @ Cluesmith',
    website: 'https://www.linkedin.com/in/waleedkadous/',
    photo: '/images/waleed.jpeg',
    time: '3:30 - 4:00 pm',
    title: 'Codev: An Operating System for AI and Humans to Work Together',
    abstract: '<p>Codev (codevos.ai) is an open source system for AI and humans to build software together. It builds on four core ideas: specs and plans as source code, multi-model review, enforced processes to deal with AI being non-deterministic, and agents coordinating the work of other agents (architect-builder pattern).<\p>Result: one engineer produced 53 PRs (with full design docs, tests, etc.) per week on a 100,000 line codebase; on a "vibe coding" task measured 1.2 points better code on a 10-point scale vs Claude Code (Opus 4.5) alone.',
    bio: 'Waleed Kadous is founder of Cluesmith and creator of Codev. Over 25 years he\'s held Principal Engineer, Senior Director, and Chief Scientist roles at Google, Uber, Canva, and Anyscale. He holds a PhD in AI from UNSW (2000), 40+ patents, and has written influential papers on LLM routing and AI for time series. He\'s currently building Multisage (multi-expert AI) and other projects alongside Codev.',
  },
  {
    id: 'speaker-lin', name: 'Lin Shi', affiliation: 'Cornell Tech', website: 'https://slimshilin.github.io/', photo: '/images/lin_shi.png', time: '4:00 - 4:30 pm',
    title: 'Evaluating Agentic Software Engineering with Terminal-Bench, Harbor Adapters, and Harbor Index',
    abstract: '<p>Evaluating coding agents is difficult because benchmarks often require different environments, harnesses, and integration logic. This talk will discuss Terminal-Bench, Harbor Adapters, and Harbor-Index as sequential efforts toward scalable and reliable agent evaluation.<\p>Terminal-Bench provides a realistic terminal-based setting for evaluating coding and tool-using agents. Harbor Adapters become the infrastructure that converts many heterogeneous benchmarks into a unified format, allowing arbitrary agents to be evaluated consistently across diverse tasks. I will present our large-scale evaluation findings, discuss observed agent capabilities and failure modes, and introduce Harbor Index, a curated set of challenging tasks designed to make broad agentic evaluation more practical and affordable.',
    bio: 'Lin Shi is a core member of Terminal Bench and team lead of Harbor Adapters, working on the evaluation, infrastructure, and datasets for language-model agents.',
  },
]

const organizers = [
  { name: 'Hao Li', website: 'https://leo-lihao.github.io', photo: '/images/haoli.jpg', affiliation: "Queen's University"},
  { name: 'Jie M. Zhang', website: 'https://sites.google.com/view/jie-zhang', photo: '/images/jiezhang.jpg', affiliation: "King's College London", objectPosition: '50% 10%' },
  { name: 'Chao Peng', website: 'https://chao-peng.github.io/', photo: '/images/peng_chao.jpg', affiliation: 'ByteDance' },
  { name: 'Shweta Garg', website: 'https://shwetagarg-dev.github.io/', photo: '/images/shweta_garg.jpg', affiliation: 'Amazon' },
  { name: 'Lingming Zhang', website: 'https://lingming.cs.illinois.edu/', photo: '/images/lingming_zhang.jpeg', affiliation: 'UIUC', objectPosition: '50% 0%'},
  { name: 'Qinghua Lu', website: 'https://people.csiro.au/L/Q/Qinghua-Lu', photo: '/images/qinghua_lu.jpg', affiliation: 'Data61, CSIRO' , objectPosition: '50% 10%'},
  { name: 'Satish Chandra', website: 'https://sites.google.com/site/schandraacmorg/', photo: '/images/satish_chandra.jpg', affiliation: 'Meta Platforms, Inc.' },
  { name: 'Thomas Zimmermann', website: 'https://thomas-zimmermann.com/', photo: '/images/thomaszimmermann.jpg', affiliation: 'UC Irvine' },
  { name: 'Ahmed E. Hassan', website: 'https://research.cs.queensu.ca/home/ahmed/home/', photo: '/images/ahmedhassan.jpg', affiliation: "Queen's University" },
]

const pc = [
  { name: 'Saima Afrin', affiliation: 'College of William and Mary' },
  { name: 'Joseph Axisa', affiliation: 'Google' },
  { name: 'Hema Sekhar Reddy Busireddy', affiliation: 'Google' },
  { name: 'Advitya Gemawat', affiliation: 'Microsoft' },
  { name: 'Jiayi Geng', affiliation: 'Carnegie Mellon University' },
  { name: 'Anwar Ghammam', affiliation: 'University of Michigan-Dearborn' },
  { name: 'Nishant Gupta', affiliation: 'Meta' },
  { name: 'Yinglong Li', affiliation: 'Google' },
  { name: 'Lintang Sutawika', affiliation: 'Carnegie Mellon University' },
  { name: 'Zehao Wang', affiliation: 'Concordia University' },
  { name: 'Haoxiang Zhang', affiliation: "Queen's University" },
  { name: 'Yu Shi', affiliation: "Queen's University", role: 'Web Chair' },
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
            <div><i class="bi bi-building"></i> DoubleTree by Hilton San Jose &middot; Room: San Jose</div>
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

  <!-- Overview 
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
  -->

  <!-- Program Schedule -->
  <section id="program" class="section">
    <div class="container">
      <div class="row mb-5">
        <div class="col-12">
          <h2 class="section-title text-center">Program Schedule</h2>
        </div>
      </div>
      <div class="program-list">
        <div class="program-item" v-for="item in programSchedule" :key="`${item.time}-${item.title}`">
          <div class="program-time">{{ item.time }}</div>
          <div class="program-details">
            <h3 class="program-title">
              <a v-if="item.speakerId" :href="'#' + item.speakerId" @click.prevent="scrollTo(item.speakerId)" class="program-title-link">{{ item.title }}</a>
              <span v-else>{{ item.title }}</span>
            </h3>
            <p v-if="item.speaker" class="program-speaker">
              <a v-if="item.speakerId" :href="'#' + item.speakerId" @click.prevent="scrollTo(item.speakerId)" class="program-speaker-link">{{ item.speaker }}</a>
              <span v-else>{{ item.speaker }}</span>
              <span v-if="item.affiliation"> ({{ item.affiliation }})</span>
            </p>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- Keynote Speakers -->
  <section id="speakers" class="section section-alt">
    <div class="container">
      <div class="row mb-5">
        <div class="col-12">
          <h2 class="section-title text-center">Keynote Speakers</h2>
        </div>
      </div>
      <div class="speakers-list">
        <div class="speaker-card" v-for="s in speakers" :key="s.name" :id="s.id">
          <div class="speaker-photo-col">
            <a v-if="s.photo && s.website" :href="s.website" target="_blank" rel="noopener noreferrer">
              <img class="speaker-photo" :src="s.photo" :alt="s.name">
            </a>
            <img v-else-if="s.photo" class="speaker-photo" :src="s.photo" :alt="s.name">
            <div v-else class="speaker-photo d-flex align-items-center justify-content-center bg-light text-muted" style="font-size: 3rem;">
              <i class="bi bi-person-fill"></i>
            </div>
            <div class="speaker-name-block">
              <h4 class="speaker-name">
                <a v-if="s.website" :href="s.website" target="_blank" rel="noopener noreferrer">{{ s.name }}</a>
                <span v-else>{{ s.name }}</span>
              </h4>
              <p class="speaker-affiliation">{{ s.affiliation }}</p>
            </div>
          </div>
          <div class="speaker-info-col">
            <p v-if="s.time" class="speaker-time"><i class="bi bi-clock"></i> {{ s.time }}</p>
            <template v-if="s.title">
              <h5 class="speaker-talk-title">{{ s.title }}</h5>
              <div class="speaker-abstract" v-html="s.abstract"></div>
              <p class="speaker-bio"><strong>Bio:</strong> {{ s.bio }}</p>
            </template>
            <p v-else class="speaker-tba">Talk details coming soon.</p>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- Submission / CTA -->
  <section id="submission" class="section section-alt">
    <div class="container">
      <div class="row">
        <div class="col-lg-4">
          <h2 class="section-title">Call for<br>Papers</h2>
        </div>
        <div class="col-lg-8">
          <hr class="section-divider d-lg-none">
          <p class="mb-5" style="font-size: 1.1rem; line-height: 1.8;">
            We offer two submission tracks covering our topics of interest:
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
              <span class="date-event" v-html="d.event"></span>
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
  <section id="pc" class="section section-alt">
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
              <span class="text-muted"> — {{ p.affiliation }}</span>
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
