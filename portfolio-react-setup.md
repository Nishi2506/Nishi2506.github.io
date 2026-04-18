# ✦ Portfolio — React/Next.js Full Project

## Folder Structure

```
portfolio/
├── public/
│   ├── cv.pdf                    ← your CV file
│   ├── transcripts/              ← PDF files
│   │   ├── msc-transcript.pdf
│   │   └── btech-transcript.pdf
│   └── avatar.jpg                ← your photo
│
├── src/
│   ├── app/                      (Next.js 14 App Router)
│   │   ├── layout.tsx
│   │   ├── page.tsx
│   │   └── globals.css
│   │
│   ├── components/
│   │   ├── layout/
│   │   │   ├── Navbar.tsx
│   │   │   └── Footer.tsx
│   │   ├── sections/
│   │   │   ├── Hero.tsx
│   │   │   ├── About.tsx
│   │   │   ├── Projects.tsx
│   │   │   ├── Resume.tsx
│   │   │   ├── Transcripts.tsx
│   │   │   ├── Skills.tsx
│   │   │   └── Contact.tsx
│   │   ├── ui/
│   │   │   ├── CustomCursor.tsx
│   │   │   ├── ParticleField.tsx
│   │   │   ├── GlassCard.tsx
│   │   │   ├── ProjectModal.tsx
│   │   │   ├── SkillBar.tsx
│   │   │   └── SectionLabel.tsx
│   │   └── three/
│   │       ├── HeroScene.tsx     ← React Three Fiber canvas
│   │       └── TorusKnot.tsx
│   │
│   ├── data/
│   │   ├── projects.ts
│   │   ├── skills.ts
│   │   └── timeline.ts
│   │
│   ├── hooks/
│   │   ├── useMousePosition.ts
│   │   ├── useScrollReveal.ts
│   │   └── useTypingEffect.ts
│   │
│   └── lib/
│       └── utils.ts
│
├── tailwind.config.ts
├── next.config.mjs
├── package.json
└── tsconfig.json
```

---

## Installation

```bash
# 1. Create Next.js app
npx create-next-app@latest portfolio \
  --typescript --tailwind --app --src-dir --import-alias "@/*"
cd portfolio

# 2. Install dependencies
npm install \
  framer-motion \
  @react-three/fiber \
  @react-three/drei \
  three \
  @types/three \
  gsap \
  @gsap/react \
  react-intersection-observer \
  react-hook-form \
  clsx \
  tailwind-merge

# 3. Run development server
npm run dev
```

---

## tailwind.config.ts

```typescript
import type { Config } from 'tailwindcss'

const config: Config = {
  content: ['./src/**/*.{js,ts,jsx,tsx,mdx}'],
  theme: {
    extend: {
      colors: {
        void:     '#07070f',
        deep:     '#0d0d1a',
        surface:  '#131320',
        pink:     '#f472b6',
        lavender: '#a78bfa',
        'soft-blue': '#60a5fa',
        teal:     '#5eead4',
      },
      fontFamily: {
        display: ['Syne', 'sans-serif'],
        body:    ['DM Sans', 'sans-serif'],
        mono:    ['Space Mono', 'monospace'],
      },
      backgroundImage: {
        'gradient-radial': 'radial-gradient(var(--tw-gradient-stops))',
        'gradient-hero': 'linear-gradient(135deg, #f472b6 0%, #a78bfa 50%, #60a5fa 100%)',
      },
      animation: {
        'float':       'float 6s ease-in-out infinite',
        'pulse-glow':  'pulseGlow 2s ease-in-out infinite',
        'blink':       'blink 1.1s step-end infinite',
        'scroll-line': 'scrollLine 2s ease-in-out infinite',
      },
      keyframes: {
        float: {
          '0%, 100%': { transform: 'translateY(0px)' },
          '50%':      { transform: 'translateY(-12px)' },
        },
        pulseGlow: {
          '0%, 100%': { boxShadow: '0 0 20px rgba(244,114,182,0.3)' },
          '50%':      { boxShadow: '0 0 40px rgba(244,114,182,0.6)' },
        },
        blink: {
          '0%, 100%': { opacity: '1' },
          '50%':      { opacity: '0' },
        },
        scrollLine: {
          '0%, 100%': { opacity: '1' },
          '50%':      { opacity: '0.3' },
        },
      },
    },
  },
  plugins: [],
}
export default config
```

---

## src/app/globals.css

```css
@import url('https://fonts.googleapis.com/css2?family=Syne:wght@400;500;600;700;800&family=DM+Sans:ital,wght@0,300;0,400;0,500;1,300&family=Space+Mono:wght@400;700&display=swap');

@tailwind base;
@tailwind components;
@tailwind utilities;

:root {
  --pink-glow:     rgba(244, 114, 182, 0.25);
  --lavender-glow: rgba(167, 139, 250, 0.20);
  --blue-glow:     rgba(96, 165, 250, 0.20);
  --teal-glow:     rgba(94, 234, 212, 0.18);
  --border-glass:  rgba(255, 255, 255, 0.08);
  --border-accent: rgba(167, 139, 250, 0.35);
}

* { cursor: none !important; }

html { scroll-behavior: smooth; scroll-padding-top: 80px; }

body {
  background: #07070f;
  color: #f1f0fb;
  overflow-x: hidden;
}

::-webkit-scrollbar       { width: 4px; }
::-webkit-scrollbar-track { background: #0d0d1a; }
::-webkit-scrollbar-thumb { background: #a78bfa; border-radius: 2px; }

.glass {
  background: rgba(255,255,255,0.04);
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
  border: 1px solid var(--border-glass);
  border-radius: 22px;
  transition: background 0.35s, border-color 0.35s, transform 0.35s, box-shadow 0.35s;
}
.glass:hover {
  background: rgba(255,255,255,0.08);
  border-color: var(--border-accent);
  transform: translateY(-4px);
  box-shadow: 0 20px 60px rgba(167,139,250,0.12);
}

.gradient-text {
  background: linear-gradient(135deg, #f472b6 0%, #a78bfa 50%, #60a5fa 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

/* Noise overlay */
body::before {
  content: '';
  position: fixed;
  inset: 0;
  background-image: url("data:image/svg+xml,...");
  pointer-events: none;
  z-index: 1000;
  opacity: 0.4;
}
```

---

## src/app/layout.tsx

```tsx
import type { Metadata } from 'next'
import './globals.css'

export const metadata: Metadata = {
  title: 'Your Name — Portfolio',
  description: 'Researcher · Developer · Creative in STEM',
  openGraph: {
    title: 'Your Name — Portfolio',
    description: 'Researcher · Developer · Creative in STEM',
    type: 'website',
  },
}

export default function RootLayout({ children }: { children: React.ReactNode }) {
  return (
    <html lang="en" className="scroll-smooth">
      <body className="bg-void text-white font-body antialiased">
        {children}
      </body>
    </html>
  )
}
```

---

## src/app/page.tsx

```tsx
'use client'
import dynamic from 'next/dynamic'
import Navbar      from '@/components/layout/Navbar'
import Footer      from '@/components/layout/Footer'
import CustomCursor from '@/components/ui/CustomCursor'
import ParticleField from '@/components/ui/ParticleField'
import About       from '@/components/sections/About'
import Projects    from '@/components/sections/Projects'
import Resume      from '@/components/sections/Resume'
import Transcripts from '@/components/sections/Transcripts'
import Skills      from '@/components/sections/Skills'
import Contact     from '@/components/sections/Contact'

// Dynamic import for Three.js (SSR disabled)
const Hero = dynamic(() => import('@/components/sections/Hero'), { ssr: false })

export default function Home() {
  return (
    <>
      <CustomCursor />
      <ParticleField />
      <Navbar />
      <main>
        <Hero />
        <About />
        <Projects />
        <Resume />
        <Transcripts />
        <Skills />
        <Contact />
      </main>
      <Footer />
    </>
  )
}
```

---

## src/components/ui/CustomCursor.tsx

```tsx
'use client'
import { useEffect, useRef, useState } from 'react'

export default function CustomCursor() {
  const dotRef  = useRef<HTMLDivElement>(null)
  const ringRef = useRef<HTMLDivElement>(null)
  const [hovered, setHovered] = useState(false)
  const mouse  = useRef({ x: 0, y: 0 })
  const ring   = useRef({ x: 0, y: 0 })
  const animId = useRef(0)

  useEffect(() => {
    const onMove = (e: MouseEvent) => {
      mouse.current = { x: e.clientX, y: e.clientY }
      if (dotRef.current) {
        dotRef.current.style.left = e.clientX + 'px'
        dotRef.current.style.top  = e.clientY + 'px'
      }
    }
    document.addEventListener('mousemove', onMove)

    const animate = () => {
      ring.current.x += (mouse.current.x - ring.current.x) * 0.12
      ring.current.y += (mouse.current.y - ring.current.y) * 0.12
      if (ringRef.current) {
        ringRef.current.style.left = ring.current.x + 'px'
        ringRef.current.style.top  = ring.current.y + 'px'
      }
      animId.current = requestAnimationFrame(animate)
    }
    animId.current = requestAnimationFrame(animate)

    const addHover = () => {
      document.querySelectorAll('a, button, [data-hover]').forEach(el => {
        el.addEventListener('mouseenter', () => setHovered(true))
        el.addEventListener('mouseleave', () => setHovered(false))
      })
    }
    addHover()

    return () => {
      document.removeEventListener('mousemove', onMove)
      cancelAnimationFrame(animId.current)
    }
  }, [])

  return (
    <>
      <div
        ref={dotRef}
        className="fixed pointer-events-none z-[9999] -translate-x-1/2 -translate-y-1/2 rounded-full transition-all duration-200"
        style={{
          width:      hovered ? 12 : 8,
          height:     hovered ? 12 : 8,
          background: hovered ? '#a78bfa' : '#f472b6',
        }}
      />
      <div
        ref={ringRef}
        className="fixed pointer-events-none z-[9998] -translate-x-1/2 -translate-y-1/2 rounded-full border transition-all duration-300"
        style={{
          width:       hovered ? 56 : 36,
          height:      hovered ? 56 : 36,
          borderColor: hovered ? '#f472b6' : '#a78bfa',
          borderWidth:  1.5,
        }}
      />
    </>
  )
}
```

---

## src/components/sections/Hero.tsx

```tsx
'use client'
import { useEffect, useRef } from 'react'
import { Canvas } from '@react-three/fiber'
import { OrbitControls, Float, MeshDistortMaterial } from '@react-three/drei'
import { motion } from 'framer-motion'
import * as THREE from 'three'
import { useTypingEffect } from '@/hooks/useTypingEffect'

function HeroMesh() {
  return (
    <Float speed={2} rotationIntensity={1.2} floatIntensity={0.8}>
      <mesh>
        <torusKnotGeometry args={[1.3, 0.38, 180, 26, 2, 3]} />
        <MeshDistortMaterial
          color="#1a1230"
          roughness={0.35}
          metalness={0.85}
          distort={0.1}
          speed={2}
        />
      </mesh>
      {/* Wireframe overlay */}
      <mesh>
        <torusKnotGeometry args={[1.3, 0.38, 80, 16, 2, 3]} />
        <meshBasicMaterial color="#a78bfa" wireframe opacity={0.12} transparent />
      </mesh>
    </Float>
  )
}

export default function Hero() {
  const taglineWords = ['Researcher', 'Developer', 'Creative', 'Builder']
  const typed = useTypingEffect(taglineWords, 90, 60, 1600)

  const container = { hidden: {}, show: { transition: { staggerChildren: 0.18 } } }
  const item = {
    hidden: { opacity: 0, y: 28 },
    show:   { opacity: 1, y: 0, transition: { duration: 0.8, ease: [0.4,0,0.2,1] } }
  }

  return (
    <section id="hero" className="relative min-h-screen flex items-center overflow-hidden">
      {/* Three.js Canvas */}
      <div className="absolute inset-0 z-0">
        <Canvas camera={{ position: [0, 0, 5], fov: 60 }} dpr={[1, 2]} gl={{ alpha: true }}>
          <ambientLight intensity={0.5} color="#111133" />
          <directionalLight position={[-2, 4, 3]} intensity={3} color="#f472b6" />
          <directionalLight position={[4, -2, -2]} intensity={2} color="#60a5fa" />
          <pointLight position={[3.5, 0, 2]} intensity={6} color="#a78bfa" />
          <HeroMesh />
        </Canvas>
      </div>

      {/* Hero Content */}
      <motion.div
        className="relative z-10 px-8 md:px-16 max-w-5xl"
        variants={container}
        initial="hidden"
        animate="show"
      >
        <motion.p
          variants={item}
          className="font-mono text-xs tracking-[0.2em] text-teal mb-6 uppercase"
        >
          // hello world — welcome to my space ✦
        </motion.p>

        <motion.h1
          variants={item}
          className="font-display font-extrabold leading-[0.95] tracking-tight mb-6"
          style={{ fontSize: 'clamp(3.5rem, 8vw, 7.5rem)' }}
        >
          <span className="gradient-text">Your<br />Name</span>
        </motion.h1>

        <motion.p
          variants={item}
          className="text-gray-400 max-w-xl mb-10 font-light"
          style={{ fontSize: 'clamp(1.1rem, 2vw, 1.4rem)', lineHeight: 1.6 }}
        >
          <span className="text-lavender font-medium">
            {typed}
            <span className="inline-block w-[3px] h-[0.9em] bg-pink-400 ml-1 align-middle rounded-sm animate-blink" />
          </span>
          {' · Developer · Creative in STEM'}
        </motion.p>

        <motion.div variants={item} className="flex gap-4 flex-wrap">
          <a href="#projects" className="btn-primary">
            ✦ View My Work
          </a>
          <a href="#contact" className="btn-ghost">
            Say hello →
          </a>
        </motion.div>
      </motion.div>

      {/* Scroll hint */}
      <div className="absolute bottom-10 left-1/2 -translate-x-1/2 flex flex-col items-center gap-2 z-10">
        <span className="font-mono text-[0.65rem] tracking-[0.14em] text-gray-600 uppercase">Scroll</span>
        <div className="w-px h-12 bg-gradient-to-b from-lavender to-transparent animate-scroll-line" />
      </div>
    </section>
  )
}
```

---

## src/hooks/useTypingEffect.ts

```typescript
import { useState, useEffect, useRef } from 'react'

export function useTypingEffect(
  words: string[],
  typeSpeed = 90,
  deleteSpeed = 60,
  pauseTime = 1600
): string {
  const [text, setText] = useState('')
  const [wordIndex, setWordIndex] = useState(0)
  const [deleting, setDeleting] = useState(false)
  const charIndex = useRef(0)

  useEffect(() => {
    const word = words[wordIndex % words.length]
    const speed = deleting ? deleteSpeed : typeSpeed

    const timer = setTimeout(() => {
      if (!deleting) {
        charIndex.current++
        setText(word.slice(0, charIndex.current))
        if (charIndex.current === word.length) {
          setTimeout(() => setDeleting(true), pauseTime)
          return
        }
      } else {
        charIndex.current--
        setText(word.slice(0, charIndex.current))
        if (charIndex.current === 0) {
          setDeleting(false)
          setWordIndex(i => i + 1)
        }
      }
    }, speed)

    return () => clearTimeout(timer)
  }, [text, deleting, wordIndex, words, typeSpeed, deleteSpeed, pauseTime])

  return text
}
```

---

## src/data/projects.ts

```typescript
export interface Project {
  id:         number
  title:      string
  description: string
  longDesc:   string
  highlights: string
  tech:       string[]
  icon:       string
  gradient:   string
  github?:    string
  demo?:      string
  paper?:     string
}

export const projects: Project[] = [
  {
    id: 0,
    title: 'Neural Style Transfer Engine',
    description: 'Real-time artistic style transfer with 4x faster inference via TensorRT.',
    longDesc: 'Custom VGG-based architecture with modified perceptual and style loss functions. Supports video input and achieves 4x faster inference through model quantization and TensorRT optimization on NVIDIA hardware.',
    highlights: 'Processed 1080p video at 24fps on RTX 3080. Integrated into a web app with 2000+ monthly users.',
    tech: ['Python', 'PyTorch', 'TensorRT', 'CUDA', 'FastAPI', 'React'],
    icon: '🧠',
    gradient: 'from-[#0f0f2e] to-[#1e0f2e]',
    github: 'https://github.com/yourhandle/neural-style',
    demo:   'https://demo.yoursite.com',
  },
  // ... add more projects
]
```

---

## src/components/sections/Skills.tsx

```tsx
'use client'
import { useInView } from 'react-intersection-observer'
import { motion } from 'framer-motion'
import SectionLabel from '@/components/ui/SectionLabel'
import { skills } from '@/data/skills'

interface SkillBarProps { name: string; pct: number; color: string; animate: boolean }

function SkillBar({ name, pct, color, animate }: SkillBarProps) {
  const gradients: Record<string, string> = {
    pink:     'from-pink-400 to-violet-400',
    lavender: 'from-violet-400 to-blue-400',
    blue:     'from-blue-400 to-teal-400',
  }
  return (
    <div className="mb-4">
      <div className="flex justify-between mb-1.5">
        <span className="text-sm font-medium text-white/90">{name}</span>
        <span className="font-mono text-xs text-white/30">{pct}%</span>
      </div>
      <div className="h-1 rounded-full bg-white/5 border border-white/5 overflow-hidden">
        <motion.div
          className={`h-full rounded-full bg-gradient-to-r ${gradients[color]}`}
          initial={{ width: 0 }}
          animate={{ width: animate ? `${pct}%` : 0 }}
          transition={{ duration: 1.2, ease: [0.4, 0, 0.2, 1], delay: 0.1 }}
        />
      </div>
    </div>
  )
}

export default function Skills() {
  const [ref, inView] = useInView({ threshold: 0.2, triggerOnce: true })

  return (
    <section id="skills" ref={ref} className="min-h-screen py-28 px-8 max-w-7xl mx-auto">
      <SectionLabel>Expertise</SectionLabel>
      <h2 className="font-display text-5xl font-bold tracking-tight mb-4">
        Skills &amp; <span className="gradient-text">Technologies</span>
      </h2>

      <div className="grid grid-cols-1 md:grid-cols-2 xl:grid-cols-4 gap-6 mt-12">
        {skills.map((cat, ci) => (
          <motion.div
            key={cat.category}
            className="glass p-7"
            initial={{ opacity: 0, y: 32 }}
            animate={inView ? { opacity: 1, y: 0 } : {}}
            transition={{ duration: 0.7, delay: ci * 0.1 }}
          >
            <p className="font-mono text-xs tracking-[0.14em] text-white/30 uppercase mb-5">
              // {cat.category}
            </p>
            {cat.skills.map(s => (
              <SkillBar key={s.name} {...s} animate={inView} />
            ))}
          </motion.div>
        ))}
      </div>
    </section>
  )
}
```

---

## src/components/sections/Contact.tsx

```tsx
'use client'
import { useState } from 'react'
import { useForm } from 'react-hook-form'
import { motion } from 'framer-motion'
import SectionLabel from '@/components/ui/SectionLabel'

interface FormData { name: string; email: string; subject: string; message: string }

const socials = [
  { icon: '⬡', label: 'GitHub',         href: 'https://github.com/yourhandle' },
  { icon: '💼', label: 'LinkedIn',       href: 'https://linkedin.com/in/yourhandle' },
  { icon: '🔬', label: 'Google Scholar', href: 'https://scholar.google.com' },
  { icon: '✉️', label: 'you@email.com',  href: 'mailto:you@email.com' },
]

export default function Contact() {
  const [sent, setSent] = useState(false)
  const { register, handleSubmit, formState: { errors } } = useForm<FormData>()

  const onSubmit = async (data: FormData) => {
    // Replace with your API endpoint / EmailJS / Resend
    await new Promise(r => setTimeout(r, 1200))
    setSent(true)
  }

  return (
    <section id="contact" className="min-h-screen py-28 px-8 max-w-7xl mx-auto">
      <SectionLabel>Get In Touch</SectionLabel>
      <h2 className="font-display text-5xl font-bold tracking-tight mb-4">
        Let's <span className="gradient-text">Connect</span>
      </h2>

      <div className="grid grid-cols-1 lg:grid-cols-2 gap-16 mt-12 items-start">
        {/* Left */}
        <div>
          <p className="text-gray-400 text-lg leading-relaxed mb-10">
            I'm always open to research collaborations, interesting opportunities,
            or just a conversation. My inbox is open.
          </p>
          <div className="flex flex-col gap-3">
            {socials.map(s => (
              <a key={s.label} href={s.href} target="_blank" rel="noreferrer"
                className="glass flex items-center gap-4 px-5 py-4 rounded-2xl text-sm text-gray-400 hover:text-white transition-all hover:translate-x-1.5">
                <span className="text-xl w-6">{s.icon}</span>
                <span className="flex-1">{s.label}</span>
                <span className="text-gray-600 text-xs">↗</span>
              </a>
            ))}
          </div>
        </div>

        {/* Form */}
        <div className="glass p-8">
          {!sent ? (
            <form onSubmit={handleSubmit(onSubmit)} className="flex flex-col gap-5">
              {[
                { id: 'name',    label: 'Your Name',    placeholder: 'Ada Lovelace',           type: 'text'  },
                { id: 'email',   label: 'Email Address', placeholder: 'ada@example.com',        type: 'email' },
                { id: 'subject', label: 'Subject',       placeholder: 'Research collaboration', type: 'text'  },
              ].map(f => (
                <div key={f.id}>
                  <label className="font-mono text-[0.68rem] tracking-[0.1em] text-white/30 uppercase block mb-1.5">
                    // {f.label}
                  </label>
                  <input
                    {...register(f.id as keyof FormData, { required: f.id !== 'subject' })}
                    type={f.type}
                    placeholder={f.placeholder}
                    className="w-full bg-white/4 border border-white/8 rounded-xl px-4 py-3 text-sm text-white placeholder:text-white/20 outline-none focus:border-lavender/50 focus:ring-2 focus:ring-lavender/10 transition-all"
                  />
                </div>
              ))}
              <div>
                <label className="font-mono text-[0.68rem] tracking-[0.1em] text-white/30 uppercase block mb-1.5">
                  // Message
                </label>
                <textarea
                  {...register('message', { required: true })}
                  placeholder="Tell me about your project or idea..."
                  rows={5}
                  className="w-full bg-white/4 border border-white/8 rounded-xl px-4 py-3 text-sm text-white placeholder:text-white/20 outline-none focus:border-lavender/50 focus:ring-2 focus:ring-lavender/10 transition-all resize-none"
                />
              </div>
              <button type="submit"
                className="btn-primary self-start mt-1">
                ✦ Send Message
              </button>
            </form>
          ) : (
            <motion.div
              initial={{ opacity: 0, scale: 0.95 }}
              animate={{ opacity: 1, scale: 1 }}
              className="text-center py-12">
              <div className="text-5xl mb-4">✓</div>
              <p className="text-teal font-medium text-lg">Message sent!</p>
              <p className="text-gray-500 text-sm mt-2">I'll get back to you soon.</p>
            </motion.div>
          )}
        </div>
      </div>
    </section>
  )
}
```

---

## Performance Optimizations

```tsx
// next.config.mjs
const nextConfig = {
  images: {
    formats: ['image/avif', 'image/webp'],
    remotePatterns: [],
  },
  experimental: {
    optimizeCss: true,
  },
}
export default nextConfig

// Lazy-load heavy sections
const Projects    = dynamic(() => import('@/components/sections/Projects'),    { loading: () => <SectionSkeleton /> })
const Transcripts = dynamic(() => import('@/components/sections/Transcripts'), { loading: () => <SectionSkeleton /> })
```

---

## Environment Variables

```env
# .env.local
NEXT_PUBLIC_EMAILJS_SERVICE_ID=your_service_id
NEXT_PUBLIC_EMAILJS_TEMPLATE_ID=your_template_id
NEXT_PUBLIC_EMAILJS_PUBLIC_KEY=your_public_key
```

---

## Deployment

```bash
# Vercel (recommended — zero config)
npm i -g vercel
vercel

# Or static export
npm run build
npm run export   # → /out folder for static hosting
```

---

## All Dependencies Summary

| Package | Purpose |
|---|---|
| `next` | Framework |
| `react`, `react-dom` | UI |
| `framer-motion` | Animations |
| `@react-three/fiber` | Three.js in React |
| `@react-three/drei` | Three.js helpers |
| `three` | 3D engine |
| `gsap` | Advanced scroll animations |
| `react-intersection-observer` | Scroll triggers |
| `react-hook-form` | Contact form |
| `tailwindcss` | Styling |
| `clsx`, `tailwind-merge` | Class utilities |
