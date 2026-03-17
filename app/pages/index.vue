<template>
  <div class="relative min-h-screen overflow-x-hidden font-sans text-slate-200 bg-[#070b13]">

    <!-- ── Background ── -->
    <div class="fixed inset-0 z-0 pointer-events-none"
      style="background: radial-gradient(ellipse 90% 70% at 15% -5%, rgba(37,99,235,0.2) 0%, transparent 60%), radial-gradient(ellipse 70% 55% at 85% 105%, rgba(109,40,217,0.16) 0%, transparent 55%), #070b13;" />
    <canvas ref="bgCanvas" class="fixed inset-0 z-0 pointer-events-none opacity-50" />
    <div class="fixed inset-0 z-0 pointer-events-none"
      style="background: radial-gradient(ellipse at center, transparent 40%, rgba(3,5,11,0.7) 100%);" />

    <!-- ── Navbar ── -->
    <nav class="fixed top-0 left-0 right-0 z-50 transition-all duration-300"
      :class="navScrolled
        ? 'bg-[rgba(7,11,19,0.94)] backdrop-blur-2xl border-b border-blue-500/10 shadow-[0_4px_32px_rgba(0,0,0,0.4)]'
        : 'bg-transparent border-b border-transparent'">
      <div class="max-w-6xl mx-auto px-6 md:px-10 h-16 flex items-center justify-between">
        <div class="flex items-center gap-2.5 cursor-default">
          <div class="w-7 h-7 rounded-lg bg-gradient-to-br from-blue-500 to-violet-600 flex items-center justify-center shadow-[0_0_16px_rgba(96,165,250,0.4)]">
            <svg width="14" height="14" viewBox="0 0 14 14" fill="none">
              <path d="M3 7h8M7 3v8" stroke="white" stroke-width="1.8" stroke-linecap="round"/>
            </svg>
          </div>
          <span class="text-[1rem] font-extrabold tracking-tight text-white">GhostlyAI</span>
          <span class="text-[0.55rem] font-bold tracking-[1.6px] bg-blue-500/10 text-blue-400 border border-blue-400/25 px-1.5 py-0.5 rounded">BETA</span>
        </div>
        <div class="hidden md:flex items-center gap-6">
          <button class="text-slate-400 hover:text-white text-[0.85rem] font-medium transition-colors" @click="scrollTo('features')">Features</button>
          <button class="text-slate-400 hover:text-white text-[0.85rem] font-medium transition-colors" @click="scrollTo('usecases')">Use Cases</button>
          <button class="text-slate-400 hover:text-white text-[0.85rem] font-medium transition-colors" @click="scrollTo('how')">How it works</button>
          <button class="text-slate-400 hover:text-white text-[0.85rem] font-medium transition-colors" @click="scrollTo('faq')">FAQ</button>
          <button
            class="ml-2 px-4 py-2 rounded-lg text-[0.82rem] font-bold text-white bg-gradient-to-r from-blue-600 to-violet-600 hover:opacity-90 transition-opacity shadow-[0_0_16px_rgba(37,99,235,0.35)]"
            @click="openModal('windows')">
            Get Early Access
          </button>
        </div>
      </div>
    </nav>

    <!-- ── Hero ── -->
    <section class="relative z-10 max-w-[860px] mx-auto px-6 md:px-10 pt-44 pb-24 text-center">

      <!-- Eyebrow -->
      <div class="inline-flex items-center gap-2.5 font-mono text-[0.74rem] text-slate-500 border border-white/8 rounded-full px-4 py-1.5 mb-10 bg-white/[0.03] reveal">
        <span class="w-[7px] h-[7px] rounded-full bg-emerald-400 animate-pulse inline-block shrink-0" />
        Powered by <strong class="text-blue-400 font-semibold">Ollama</strong>&nbsp;·&nbsp;Runs 100% on your machine
      </div>

      <!-- Title -->
      <h1 class="font-extrabold leading-[1.14] tracking-[-0.045em] text-[#eef2ff] mb-7" style="font-size: clamp(2.4rem, 5.5vw, 4rem);">
        <span class="block reveal" style="--d:0.04s">The invisible AI</span>
        <span class="block reveal bg-gradient-to-r from-blue-400 via-indigo-300 to-violet-400 bg-clip-text text-transparent" style="--d:0.16s">that sees your screen.</span>
      </h1>

      <!-- Sub -->
      <p class="leading-[1.82] text-slate-400 max-w-[600px] mx-auto mb-10 reveal" style="font-size: clamp(1rem, 2vw, 1.1rem); --d:0.28s">
        GhostlyAI is a desktop overlay powered by local AI — it reads your screen in real time, coaches you through interviews, explains code, summarises documents, and answers any question.
        <em class="not-italic font-semibold text-indigo-200/90">Zero trace. Zero cloud. Zero compromise.</em>
      </p>

      <!-- CTAs -->
      <div class="flex gap-3 justify-center flex-wrap mb-5 reveal" style="--d:0.38s">
        <button
          class="inline-flex items-center gap-2.5 px-6 py-3.5 rounded-xl text-[0.9rem] font-bold text-white bg-gradient-to-br from-blue-600 to-violet-600 shadow-[0_0_0_1px_rgba(96,165,250,0.15),0_8px_28px_rgba(37,99,235,0.35)] hover:-translate-y-0.5 hover:shadow-[0_0_0_1px_rgba(96,165,250,0.3),0_14px_36px_rgba(37,99,235,0.45)] transition-all duration-200"
          @click="openModal('windows')">
          <svg width="14" height="14" viewBox="0 0 14 14" fill="currentColor"><path d="M0 0h6v6H0zM8 0h6v6H8zM0 8h6v6H0zM8 8h6v6H8z"/></svg>
          Download for Windows
          <span class="text-[0.6rem] font-bold tracking-[0.8px] uppercase bg-white/[0.15] px-2 py-0.5 rounded-full">Soon</span>
        </button>
        <button
          class="inline-flex items-center gap-2.5 px-6 py-3.5 rounded-xl text-[0.9rem] font-bold text-slate-200 bg-white/[0.05] border border-white/[0.1] hover:bg-white/[0.09] hover:-translate-y-0.5 transition-all duration-200"
          @click="openModal('mac')">
          <svg width="15" height="15" viewBox="0 0 15 15" fill="currentColor"><path d="M10.8 1.2c-1.2 0-2.1.7-2.8 1.5C7.3 1.9 6.4 1.2 5.2 1.2 3 1.2 1 3.2 1 5.6 1 9.7 7.8 14 7.8 14s6.9-4.3 6.9-8.4c0-2.4-1.9-4.4-3.9-4.4z"/></svg>
          Download for macOS
          <span class="text-[0.6rem] font-bold tracking-[0.8px] uppercase bg-white/[0.15] px-2 py-0.5 rounded-full">Soon</span>
        </button>
      </div>

      <p class="font-mono text-[0.67rem] text-slate-600 reveal" style="--d:0.46s">
        Free &amp; open source · No sign-up · Your data never leaves your device
      </p>

      <!-- Stats bar -->
      <div class="mt-12 mx-auto max-w-[560px] grid grid-cols-3 gap-px bg-white/[0.06] rounded-2xl overflow-hidden border border-white/[0.06] reveal" style="--d:0.56s">
        <div v-for="s in stats" :key="s.label" class="bg-[#070b13] px-6 py-4 text-center">
          <div class="text-xl font-extrabold tracking-tight text-white mb-0.5">{{ s.value }}</div>
          <div class="font-mono text-[0.65rem] text-slate-600">{{ s.label }}</div>
        </div>
      </div>

      <!-- Mock overlay window -->
      <div class="mt-14 mx-auto max-w-[560px] rounded-2xl overflow-hidden border border-blue-400/[0.13] bg-[rgba(8,13,26,0.97)] shadow-[0_0_0_1px_rgba(255,255,255,0.04),0_40px_80px_rgba(0,0,0,0.6)] reveal" style="--d:0.66s">
        <!-- Title bar -->
        <div class="flex items-center gap-1.5 px-4 py-2.5 bg-white/[0.025] border-b border-white/[0.05] font-mono text-[0.68rem]">
          <span class="w-2.5 h-2.5 rounded-full bg-[#ff5f57] inline-block" />
          <span class="w-2.5 h-2.5 rounded-full bg-[#febc2e] inline-block" />
          <span class="w-2.5 h-2.5 rounded-full bg-[#28c840] inline-block" />
          <span class="flex-1 text-center text-slate-600">GhostlyAI — Overlay Mode</span>
          <span class="text-emerald-400 text-[0.64rem] font-bold flex items-center gap-1">
            <span class="w-1.5 h-1.5 rounded-full bg-emerald-400 inline-block animate-pulse" />LIVE
          </span>
        </div>
        <!-- Context bar -->
        <div class="flex items-center gap-2 px-4 py-2 bg-blue-500/[0.04] border-b border-blue-400/[0.08]">
          <span class="font-mono text-[0.6rem] text-slate-600">CONTEXT DETECTED</span>
          <span class="font-mono text-[0.6rem] text-blue-400 bg-blue-400/10 px-1.5 py-0.5 rounded">📹 Video Interview · Zoom</span>
          <span class="font-mono text-[0.6rem] text-violet-400 bg-violet-400/10 px-1.5 py-0.5 rounded">💻 Code Editor · VS Code</span>
        </div>
        <!-- Chat -->
        <div class="p-4 flex flex-col gap-3">
          <div class="max-w-[88%] self-start bg-blue-400/[0.07] border border-blue-400/[0.14] rounded-2xl rounded-tl-sm p-3.5 text-[0.81rem] leading-relaxed flex flex-col gap-1.5">
            <span class="text-[0.58rem] font-bold tracking-[0.6px] opacity-50 uppercase">GhostlyAI</span>
            I can see the interviewer's question: <em class="not-italic text-blue-300">"Tell me about a time you resolved a technical conflict."</em> Here's a strong STAR response using your background...
          </div>
          <div class="max-w-[75%] self-end bg-violet-600/[0.1] border border-violet-500/[0.18] rounded-2xl rounded-tr-sm p-3.5 text-[0.81rem] leading-relaxed flex flex-col gap-1.5">
            <span class="text-[0.58rem] font-bold tracking-[0.6px] opacity-50 uppercase">You</span>
            What does the function on line 42 do?
          </div>
          <div class="max-w-[88%] self-start bg-blue-400/[0.07] border border-blue-400/[0.14] rounded-2xl rounded-tl-sm p-3.5 text-[0.81rem] leading-relaxed flex flex-col gap-1.5">
            <span class="text-[0.58rem] font-bold tracking-[0.6px] opacity-50 uppercase">GhostlyAI</span>
            <span class="flex gap-1.5 py-0.5">
              <i class="w-1.5 h-1.5 rounded-full bg-blue-400 not-italic inline-block animate-[blink_1.2s_ease-in-out_infinite]" />
              <i class="w-1.5 h-1.5 rounded-full bg-blue-400 not-italic inline-block animate-[blink_1.2s_ease-in-out_0.2s_infinite]" />
              <i class="w-1.5 h-1.5 rounded-full bg-blue-400 not-italic inline-block animate-[blink_1.2s_ease-in-out_0.4s_infinite]" />
            </span>
          </div>
        </div>
        <!-- Footer -->
        <div class="px-4 py-2 flex items-center justify-between border-t border-white/[0.04] font-mono text-[0.65rem]">
          <span class="flex items-center gap-1.5 text-emerald-400/80">
            <span class="w-1.5 h-1.5 rounded-full bg-emerald-400 inline-block" />
            Hidden from OBS · Zoom · Teams · Loom · Meets
          </span>
          <span class="text-slate-600">llama3.2 · local · 0ms latency</span>
        </div>
      </div>
    </section>

    <!-- ── Social proof ── -->
    <section class="relative z-10 border-y border-white/[0.04] bg-white/[0.015] py-5">
      <div class="max-w-5xl mx-auto px-8">
        <p class="font-mono text-[0.62rem] tracking-[2.5px] text-slate-600 text-center mb-5">WORKS INVISIBLY INSIDE</p>
        <div class="flex flex-wrap justify-center items-center gap-x-10 gap-y-4">
          <span v-for="app in compatApps" :key="app" class="text-slate-500 text-sm font-semibold tracking-wide">{{ app }}</span>
        </div>
      </div>
    </section>

    <!-- ── Features ── -->
    <section id="features" class="relative z-10 max-w-6xl mx-auto px-6 md:px-10 py-28">
      <div class="mb-16">
        <p class="font-mono text-[0.64rem] tracking-[3px] text-slate-600 mb-3 reveal">CORE FEATURES</p>
        <h2 class="font-extrabold tracking-[-0.04em] leading-[1.16] text-[#eef2ff] reveal" style="font-size: clamp(1.7rem, 3.5vw, 2.6rem); --d:0.08s">
          Everything you need.<br>
          <span class="text-slate-500 font-semibold">Nothing anyone can see.</span>
        </h2>
      </div>
      <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
        <div
          v-for="(feat, i) in features"
          :key="feat.title"
          class="group relative bg-white/[0.02] border border-white/[0.065] rounded-2xl p-6 overflow-hidden transition-all duration-300 hover:-translate-y-1.5 hover:border-blue-400/25 hover:shadow-[0_16px_48px_rgba(0,0,0,0.35)] reveal"
          :class="feat.wide ? 'md:col-span-2' : ''"
          :style="`--d:${0.05 * i}s`"
        >
          <div class="absolute inset-0 rounded-2xl bg-gradient-to-br from-blue-500/[0.06] to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300 pointer-events-none" />
          <div class="w-11 h-11 rounded-xl bg-blue-500/[0.08] border border-blue-400/[0.12] flex items-center justify-center mb-5 group-hover:border-blue-400/25 transition-colors duration-300" v-html="feat.icon" />
          <h3 class="text-[0.95rem] font-bold tracking-tight text-[#e8eeff] mb-2 leading-snug">{{ feat.title }}</h3>
          <p class="text-[0.83rem] text-slate-500 leading-[1.72]">{{ feat.desc }}</p>
          <span v-if="feat.tag" class="inline-block mt-3.5 text-[0.58rem] font-bold tracking-[1.2px] uppercase px-2 py-0.5 rounded-full bg-blue-400/[0.08] text-blue-400 border border-blue-400/[0.16]">{{ feat.tag }}</span>
        </div>
      </div>
    </section>

    <!-- ── Use Cases ── -->
    <section id="usecases" class="relative z-10 border-t border-white/[0.04] py-28">
      <div class="max-w-6xl mx-auto px-6 md:px-10">
        <div class="mb-16">
          <p class="font-mono text-[0.64rem] tracking-[3px] text-slate-600 mb-3 reveal">USE CASES</p>
          <h2 class="font-extrabold tracking-[-0.04em] leading-[1.16] text-[#eef2ff] reveal" style="font-size: clamp(1.7rem, 3.5vw, 2.6rem); --d:0.08s">
            One tool. Every situation.
          </h2>
        </div>
        <div class="grid grid-cols-1 md:grid-cols-2 gap-5">
          <div
            v-for="(uc, i) in useCases"
            :key="uc.title"
            class="group flex gap-5 bg-white/[0.02] border border-white/[0.065] rounded-2xl p-6 transition-all duration-300 hover:border-blue-400/20 hover:bg-white/[0.035] reveal"
            :style="`--d:${0.07 * i}s`"
          >
            <div class="text-2xl shrink-0 mt-0.5">{{ uc.emoji }}</div>
            <div>
              <div class="flex items-center gap-2.5 mb-2">
                <h3 class="text-[0.95rem] font-bold tracking-tight text-[#e8eeff]">{{ uc.title }}</h3>
                <span v-if="uc.badge" class="text-[0.56rem] font-bold tracking-[1px] uppercase px-1.5 py-0.5 rounded bg-emerald-400/10 text-emerald-400 border border-emerald-400/20">{{ uc.badge }}</span>
              </div>
              <p class="text-[0.83rem] text-slate-500 leading-[1.7]">{{ uc.desc }}</p>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- ── How it works ── -->
    <section id="how" class="relative z-10 border-t border-white/[0.04] py-28">
      <div class="max-w-6xl mx-auto px-6 md:px-10">
        <div class="mb-16">
          <p class="font-mono text-[0.64rem] tracking-[3px] text-slate-600 mb-3 reveal">HOW IT WORKS</p>
          <h2 class="font-extrabold tracking-[-0.04em] leading-[1.16] text-[#eef2ff] reveal" style="font-size: clamp(1.7rem, 3.5vw, 2.6rem); --d:0.08s">
            Up in 3 minutes.<br>
            <span class="text-slate-500 font-semibold">Running forever after.</span>
          </h2>
        </div>
        <div class="grid grid-cols-1 md:grid-cols-3 gap-5">
          <div
            v-for="(step, i) in steps"
            :key="i"
            class="relative bg-white/[0.018] border border-white/[0.06] rounded-2xl p-7 transition-all duration-300 hover:-translate-y-1 hover:border-blue-400/[0.18] reveal"
            :style="`--d:${0.1 * i}s`"
          >
            <div class="absolute top-5 right-6 font-mono text-[2.8rem] font-light leading-none select-none" style="color: rgba(96,165,250,0.08)">0{{ i + 1 }}</div>
            <div class="w-9 h-9 rounded-xl bg-gradient-to-br flex items-center justify-center mb-5 text-base"
              :style="`background: ${step.bg}`">{{ step.icon }}</div>
            <h4 class="text-[0.95rem] font-bold tracking-tight text-[#e8eeff] mb-2.5">{{ step.title }}</h4>
            <p class="text-[0.83rem] text-slate-500 leading-[1.66]">{{ step.desc }}</p>
            <div v-if="step.code" class="mt-4 bg-black/40 border border-white/[0.06] rounded-lg px-3 py-2 font-mono text-[0.72rem] text-blue-300">{{ step.code }}</div>
          </div>
        </div>
      </div>
    </section>

    <!-- ── Privacy banner ── -->
    <section class="relative z-10 max-w-6xl mx-auto px-6 md:px-10 pb-28">
      <div class="relative overflow-hidden rounded-3xl border border-blue-400/[0.16] p-10 md:p-14 reveal"
        style="background: linear-gradient(135deg, rgba(37,99,235,0.1) 0%, rgba(109,40,217,0.08) 100%);">
        <div class="absolute -top-20 -right-20 w-64 h-64 rounded-full opacity-20 pointer-events-none"
          style="background: radial-gradient(circle, rgba(96,165,250,0.4), transparent 70%)" />
        <div class="relative z-10 flex flex-col md:flex-row md:items-center gap-8">
          <div class="shrink-0">
            <div class="w-16 h-16 rounded-2xl bg-blue-500/10 border border-blue-400/20 flex items-center justify-center">
              <svg width="32" height="32" viewBox="0 0 32 32" fill="none">
                <path d="M16 2L4 7v8c0 7.2 5.2 13.9 12 15.5C22.8 28.9 28 22.2 28 15V7L16 2z" stroke="#60a5fa" stroke-width="1.8" fill="none"/>
                <path d="M10 16l4 4 8-8" stroke="#60a5fa" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"/>
              </svg>
            </div>
          </div>
          <div class="flex-1">
            <h3 class="text-[1.4rem] font-extrabold tracking-tight text-[#e8eeff] mb-3">100% local. 100% private. Always.</h3>
            <p class="text-[0.88rem] text-slate-400 leading-[1.78] max-w-2xl">
              GhostlyAI runs entirely on your machine using Ollama. No data is sent to any server — ever.
              Your screen contents, your conversations, your context: all of it stays on your device.
              No API keys to manage, no subscriptions, no usage logs. Just pure, offline AI.
            </p>
          </div>
          <div class="shrink-0 flex flex-col gap-3">
            <div v-for="p in privacyPoints" :key="p" class="flex items-center gap-2.5 text-[0.8rem] text-slate-400">
              <span class="w-4 h-4 rounded-full bg-emerald-400/15 border border-emerald-400/30 flex items-center justify-center shrink-0">
                <svg width="8" height="8" viewBox="0 0 8 8" fill="none"><path d="M1 4l2 2 4-4" stroke="#34d399" stroke-width="1.4" stroke-linecap="round"/></svg>
              </span>
              {{ p }}
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- ── Testimonials ── -->
    <section class="relative z-10 border-t border-white/[0.04] py-28">
      <div class="max-w-6xl mx-auto px-6 md:px-10">
        <div class="mb-14">
          <p class="font-mono text-[0.64rem] tracking-[3px] text-slate-600 mb-3 reveal">EARLY FEEDBACK</p>
          <h2 class="font-extrabold tracking-[-0.04em] leading-[1.16] text-[#eef2ff] reveal" style="font-size: clamp(1.7rem, 3.5vw, 2.6rem); --d:0.08s">
            What testers are saying.
          </h2>
        </div>
        <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
          <div
            v-for="(t, i) in testimonials"
            :key="i"
            class="bg-white/[0.02] border border-white/[0.065] rounded-2xl p-6 flex flex-col gap-4 reveal"
            :style="`--d:${0.07 * i}s`"
          >
            <div class="flex gap-0.5">
              <span v-for="s in 5" :key="s" class="text-amber-400 text-sm">★</span>
            </div>
            <p class="text-[0.86rem] text-slate-400 leading-[1.72] flex-1">"{{ t.quote }}"</p>
            <div class="flex items-center gap-3 pt-2 border-t border-white/[0.05]">
              <div class="w-8 h-8 rounded-full flex items-center justify-center text-sm font-bold text-white"
                :style="`background: ${t.color}`">{{ t.name[0] }}</div>
              <div>
                <div class="text-[0.82rem] font-semibold text-slate-300">{{ t.name }}</div>
                <div class="text-[0.72rem] text-slate-600">{{ t.role }}</div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- ── FAQ ── -->
    <section id="faq" class="relative z-10 border-t border-white/[0.04] py-28">
      <div class="max-w-[740px] mx-auto px-6 md:px-10">
        <p class="font-mono text-[0.64rem] tracking-[3px] text-slate-600 mb-3 reveal">FAQ</p>
        <h2 class="font-extrabold tracking-[-0.04em] leading-[1.16] text-[#eef2ff] mb-10 reveal" style="font-size: clamp(1.7rem, 3.5vw, 2.6rem); --d:0.08s">
          Got questions?
        </h2>
        <div class="flex flex-col divide-y divide-white/[0.06]">
          <div
            v-for="(q, i) in faqs"
            :key="i"
            class="reveal"
            :style="`--d:${0.05 * i}s`"
          >
            <button
              class="w-full flex justify-between items-start gap-4 py-5 px-1 text-left transition-colors duration-200 group"
              @click="toggleFaq(i)"
            >
              <span class="text-[0.94rem] font-semibold tracking-tight leading-snug transition-colors duration-200"
                :class="openFaq === i ? 'text-blue-400' : 'text-slate-300 group-hover:text-white'">
                {{ q.q }}
              </span>
              <span
                class="shrink-0 w-6 h-6 rounded-full border flex items-center justify-center text-base font-light transition-all duration-300 mt-0.5"
                :class="openFaq === i
                  ? 'border-blue-400/40 text-blue-400 rotate-45'
                  : 'border-white/10 text-slate-600 group-hover:border-white/20 group-hover:text-slate-400'"
              >+</span>
            </button>
            <div
              class="overflow-hidden transition-all duration-300 ease-in-out px-1"
              :style="openFaq === i ? 'max-height:300px; opacity:1; padding-bottom:20px;' : 'max-height:0px; opacity:0; padding-bottom:0;'"
            >
              <p class="text-[0.85rem] text-slate-500 leading-[1.78]">{{ q.a }}</p>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- ── CTA banner ── -->
    <section class="relative z-10 max-w-6xl mx-auto px-6 md:px-10 pb-28">
      <div class="relative overflow-hidden rounded-3xl text-center py-20 px-8 border border-white/[0.07] reveal"
        style="background: linear-gradient(135deg, rgba(37,99,235,0.12), rgba(109,40,217,0.1));">
        <div class="absolute inset-0 pointer-events-none"
          style="background: radial-gradient(ellipse 80% 80% at 50% 120%, rgba(96,165,250,0.12), transparent 70%)" />
        <div class="relative z-10">
          <p class="font-mono text-[0.64rem] tracking-[3px] text-blue-400/60 mb-4">GET NOTIFIED</p>
          <h2 class="font-extrabold tracking-[-0.04em] leading-[1.16] text-[#eef2ff] mb-4" style="font-size: clamp(1.8rem, 4vw, 3rem);">
            Be first in line.
          </h2>
          <p class="text-slate-400 mb-10 max-w-lg mx-auto" style="font-size: 1rem; line-height: 1.75;">
            GhostlyAI is launching soon for Windows and macOS. Drop your email and we'll ping you the moment it ships.
          </p>
          <div class="flex gap-3 flex-wrap justify-center">
            <button
              class="inline-flex items-center gap-2.5 px-7 py-3.5 rounded-xl text-[0.9rem] font-bold text-white bg-gradient-to-br from-blue-600 to-violet-600 shadow-[0_0_0_1px_rgba(96,165,250,0.15),0_8px_28px_rgba(37,99,235,0.4)] hover:-translate-y-0.5 transition-all duration-200"
              @click="openModal('windows')">
              <svg width="14" height="14" viewBox="0 0 14 14" fill="currentColor"><path d="M0 0h6v6H0zM8 0h6v6H8zM0 8h6v6H0zM8 8h6v6H8z"/></svg>
              Notify me for Windows
            </button>
            <button
              class="inline-flex items-center gap-2.5 px-7 py-3.5 rounded-xl text-[0.9rem] font-bold text-slate-200 bg-white/[0.06] border border-white/10 hover:bg-white/[0.1] hover:-translate-y-0.5 transition-all duration-200"
              @click="openModal('mac')">
              <svg width="15" height="15" viewBox="0 0 15 15" fill="currentColor"><path d="M10.8 1.2c-1.2 0-2.1.7-2.8 1.5C7.3 1.9 6.4 1.2 5.2 1.2 3 1.2 1 3.2 1 5.6 1 9.7 7.8 14 7.8 14s6.9-4.3 6.9-8.4c0-2.4-1.9-4.4-3.9-4.4z"/></svg>
              Notify me for macOS
            </button>
          </div>
        </div>
      </div>
    </section>

    <!-- ── Footer ── -->
    <footer class="relative z-10 bg-[#050810] border-t border-white/[0.05]">
      <div class="max-w-6xl mx-auto px-6 md:px-10 py-12">
        <div class="flex flex-col md:flex-row justify-between gap-10 mb-10">
          <!-- Brand -->
          <div class="max-w-xs">
            <div class="flex items-center gap-2.5 mb-3">
              <div class="w-7 h-7 rounded-lg bg-gradient-to-br from-blue-500 to-violet-600 flex items-center justify-center">
                <svg width="14" height="14" viewBox="0 0 14 14" fill="none">
                  <path d="M3 7h8M7 3v8" stroke="white" stroke-width="1.8" stroke-linecap="round"/>
                </svg>
              </div>
              <span class="text-[1rem] font-extrabold tracking-tight text-white">GhostlyAI</span>
            </div>
            <p class="text-[0.82rem] text-slate-600 leading-[1.7]">A private, offline AI overlay for your desktop. See your screen. Answer anything. Stay invisible.</p>
          </div>
          <!-- Links -->
          <div class="flex gap-16">
            <div>
              <p class="font-mono text-[0.6rem] tracking-[2px] text-slate-700 mb-4">PRODUCT</p>
              <div class="flex flex-col gap-2.5">
                <button class="text-[0.82rem] text-slate-500 hover:text-slate-300 text-left transition-colors" @click="scrollTo('features')">Features</button>
                <button class="text-[0.82rem] text-slate-500 hover:text-slate-300 text-left transition-colors" @click="scrollTo('usecases')">Use Cases</button>
                <button class="text-[0.82rem] text-slate-500 hover:text-slate-300 text-left transition-colors" @click="scrollTo('how')">How it works</button>
              </div>
            </div>
            <div>
              <p class="font-mono text-[0.6rem] tracking-[2px] text-slate-700 mb-4">OPEN SOURCE</p>
              <div class="flex flex-col gap-2.5">
                <a href="https://github.com/surelle-ha" target="_blank" rel="noopener" class="text-[0.82rem] text-slate-500 hover:text-slate-300 transition-colors">GitHub</a>
                <a href="#" class="text-[0.82rem] text-slate-500 hover:text-slate-300 transition-colors">Changelog</a>
                <a href="#" class="text-[0.82rem] text-slate-500 hover:text-slate-300 transition-colors">Roadmap</a>
              </div>
            </div>
          </div>
        </div>
        <div class="pt-6 border-t border-white/[0.05] flex flex-col md:flex-row items-center justify-between gap-3">
          <span class="text-[0.78rem] text-slate-700">
            Built by <a href="https://github.com/surelle-ha" target="_blank" rel="noopener" class="text-blue-400/70 hover:text-blue-400 transition-colors">surelle-ha</a>
          </span>
          <span class="font-mono text-[0.65rem] text-slate-800">© 2025 GhostlyAI · MIT License · Open Source</span>
        </div>
      </div>
    </footer>

    <!-- ── Modal ── -->
    <ClientOnly>
      <Teleport to="body">
        <Transition
          enter-active-class="transition-all duration-200 ease-out"
          enter-from-class="opacity-0"
          enter-to-class="opacity-100"
          leave-active-class="transition-all duration-150 ease-in"
          leave-from-class="opacity-100"
          leave-to-class="opacity-0"
        >
          <div v-if="modalOpen" class="fixed inset-0 z-[200] bg-black/80 backdrop-blur-2xl flex items-center justify-center p-8" @click.self="modalOpen = false">
            <Transition
              enter-active-class="transition-all duration-220 ease-out"
              enter-from-class="opacity-0 scale-95 translate-y-3"
              enter-to-class="opacity-100 scale-100 translate-y-0"
            >
              <div v-if="modalOpen" class="bg-[#0b1022] border border-blue-400/20 rounded-2xl p-10 max-w-[420px] w-full text-center relative shadow-[0_0_0_1px_rgba(255,255,255,0.03),0_40px_80px_rgba(0,0,0,0.75)]">
                <button class="absolute top-4 right-4 w-7 h-7 rounded-full bg-white/5 hover:bg-white/10 text-slate-500 hover:text-white text-sm transition-all flex items-center justify-center" @click="modalOpen = false">✕</button>
                <div class="w-14 h-14 rounded-2xl bg-blue-500/10 border border-blue-400/20 flex items-center justify-center mx-auto mb-5">
                  <svg v-if="modalPlatform === 'windows'" width="28" height="28" viewBox="0 0 28 28" fill="#60a5fa">
                    <rect x="1" y="1" width="12" height="12" rx="2"/><rect x="15" y="1" width="12" height="12" rx="2"/>
                    <rect x="1" y="15" width="12" height="12" rx="2"/><rect x="15" y="15" width="12" height="12" rx="2"/>
                  </svg>
                  <svg v-else width="28" height="28" viewBox="0 0 28 28" fill="#60a5fa">
                    <path d="M20 2c-2.3 0-4 1.7-5.3 3.2C13.4 3.7 11.7 2 9.4 2 5.4 2 2 5.6 2 9.8c0 6.8 12 17.2 12 17.2s12-10.4 12-17.2c0-4.2-2.6-7.8-6-7.8z"/>
                  </svg>
                </div>
                <h3 class="text-xl font-extrabold tracking-tight text-[#e8eeff] mb-2">
                  Coming soon for {{ modalPlatform === 'windows' ? 'Windows' : 'macOS' }}
                </h3>
                <p class="text-[0.86rem] text-slate-500 mb-6 leading-relaxed">
                  We'll send you one email the moment GhostlyAI is ready to download. No spam, ever.
                </p>
                <div class="flex gap-2 mb-3">
                  <input
                    v-model="emailVal"
                    type="email"
                    placeholder="your@email.com"
                    class="flex-1 px-4 py-2.5 rounded-lg bg-white/[0.05] border border-white/10 text-slate-200 text-sm placeholder-slate-600 outline-none focus:border-blue-400/50 transition-colors font-sans"
                    @keyup.enter="submitEmail"
                  />
                  <button
                    class="px-4 py-2.5 rounded-lg bg-gradient-to-br from-blue-600 to-violet-600 text-white text-sm font-bold hover:opacity-90 transition-opacity whitespace-nowrap"
                    @click="submitEmail">
                    Notify Me
                  </button>
                </div>
                <Transition enter-active-class="transition-all duration-300" enter-from-class="opacity-0 -translate-y-1" enter-to-class="opacity-100 translate-y-0">
                  <p v-if="submitted" class="text-emerald-400 font-semibold text-sm mb-2">🎉 You're on the early access list!</p>
                </Transition>
                <p class="font-mono text-[0.65rem] text-slate-700">No spam · Unsubscribe anytime · One email only</p>
              </div>
            </Transition>
          </div>
        </Transition>
      </Teleport>
    </ClientOnly>

  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const modalOpen = ref(false)
const modalPlatform = ref('windows')
const emailVal = ref('')
const submitted = ref(false)
const openFaq = ref(null)
const navScrolled = ref(false)
const bgCanvas = ref(null)

function scrollTo(id) {
  const el = document.getElementById(id)
  if (el) el.scrollIntoView({ behavior: 'smooth', block: 'start' })
}
function onScroll() { navScrolled.value = window.scrollY > 40 }
function toggleFaq(i) { openFaq.value = openFaq.value === i ? null : i }
function openModal(platform) {
  modalPlatform.value = platform
  submitted.value = false
  emailVal.value = ''
  modalOpen.value = true
}
function submitEmail() {
  if (emailVal.value.includes('@')) {
    submitted.value = true
    emailVal.value = ''
  }
}

let revealObserver = null
function initReveal() {
  revealObserver = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.add('is-revealed')
        revealObserver.unobserve(entry.target)
      }
    })
  }, { threshold: 0.08 })
  document.querySelectorAll('.reveal').forEach(el => revealObserver.observe(el))
}

function initCanvas() {
  const canvas = bgCanvas.value
  if (!canvas) return
  const ctx = canvas.getContext('2d')
  let W, H, particles, animId
  function resize() { W = canvas.width = window.innerWidth; H = canvas.height = window.innerHeight }
  function makeParticles() {
    particles = Array.from({ length: 60 }, () => ({
      x: Math.random() * W, y: Math.random() * H,
      r: Math.random() * 1.6 + 0.3,
      dx: (Math.random() - 0.5) * 0.2,
      dy: (Math.random() - 0.5) * 0.2,
      o: Math.random() * 0.45 + 0.08,
    }))
  }
  function draw() {
    ctx.clearRect(0, 0, W, H)
    particles.forEach(p => {
      ctx.beginPath(); ctx.arc(p.x, p.y, p.r, 0, Math.PI * 2)
      ctx.fillStyle = `rgba(96,165,250,${p.o})`; ctx.fill()
      p.x += p.dx; p.y += p.dy
      if (p.x < 0) p.x = W; if (p.x > W) p.x = 0
      if (p.y < 0) p.y = H; if (p.y > H) p.y = 0
    })
    for (let i = 0; i < particles.length; i++) {
      for (let j = i + 1; j < particles.length; j++) {
        const a = particles[i], b = particles[j]
        const d = Math.hypot(a.x - b.x, a.y - b.y)
        if (d < 140) {
          ctx.beginPath(); ctx.moveTo(a.x, a.y); ctx.lineTo(b.x, b.y)
          ctx.strokeStyle = `rgba(96,165,250,${0.065 * (1 - d / 140)})`
          ctx.lineWidth = 0.5; ctx.stroke()
        }
      }
    }
    animId = requestAnimationFrame(draw)
  }
  resize(); makeParticles(); draw()
  window.addEventListener('resize', () => { resize(); makeParticles() })
  return () => cancelAnimationFrame(animId)
}

let cancelCanvas = null
onMounted(() => {
  window.addEventListener('scroll', onScroll, { passive: true })
  initReveal()
  cancelCanvas = initCanvas()
})
onUnmounted(() => {
  window.removeEventListener('scroll', onScroll)
  if (revealObserver) revealObserver.disconnect()
  if (cancelCanvas) cancelCanvas()
})

/* ── Data ── */
const stats = [
  { value: '100%', label: 'offline · local' },
  { value: '0ms', label: 'cloud latency' },
  { value: '∞', label: 'models supported' },
]

const compatApps = ['Zoom', 'Microsoft Teams', 'Google Meet', 'OBS Studio', 'Loom', 'Discord', 'Slack Huddles', 'Webex']

const features = [
  {
    title: 'Invisible Screen Overlay',
    desc: 'Renders on a special window layer excluded from all screen capture APIs. OBS, Zoom, Teams, Loom — none of them will see it.',
    icon: '<svg width="22" height="22" viewBox="0 0 24 24" fill="none"><path d="M2 12s3.6-7 10-7 10 7 10 7-3.6 7-10 7-10-7-10-7z" stroke="#60a5fa" stroke-width="1.6" fill="none"/><circle cx="12" cy="12" r="3" fill="#60a5fa" opacity="0.3"/><path d="M3 3l18 18" stroke="#60a5fa" stroke-width="1.6" stroke-linecap="round" opacity="0.4"/></svg>',
    tag: 'Core', wide: true,
  },
  {
    title: 'Real-Time Screen Reading',
    desc: 'OCR + vision models parse everything on your screen — code, slides, browser, documents — in milliseconds.',
    icon: '<svg width="22" height="22" viewBox="0 0 24 24" fill="none"><rect x="2" y="3" width="20" height="14" rx="2.5" stroke="#60a5fa" stroke-width="1.6" fill="none"/><path d="M7 21h10M12 17v4" stroke="#60a5fa" stroke-width="1.6" stroke-linecap="round"/><path d="M6 9h4M14 7.5h4M6 12h8" stroke="#60a5fa" stroke-width="1.3" stroke-linecap="round" opacity="0.5"/></svg>',
    tag: null, wide: false,
  },
  {
    title: 'Interview Copilot',
    desc: 'Live question detection, STAR-structured answer suggestions, and follow-up prompts — all in real time, invisible to interviewers.',
    icon: '<svg width="22" height="22" viewBox="0 0 24 24" fill="none"><path d="M3 5h18a2 2 0 012 2v9a2 2 0 01-2 2H3a2 2 0 01-2-2V7a2 2 0 012-2z" stroke="#60a5fa" stroke-width="1.6" fill="none"/><path d="M7 20l2-2h6l2 2" stroke="#60a5fa" stroke-width="1.6" stroke-linecap="round"/><circle cx="12" cy="11" r="2.5" stroke="#60a5fa" stroke-width="1.4"/></svg>',
    tag: 'Popular', wide: false,
  },
  {
    title: 'Offline Local LLM',
    desc: 'GhostlyAI talks directly to your Ollama instance. Llama 3, Mistral, Gemma, DeepSeek — your choice, your hardware, your rules.',
    icon: '<svg width="22" height="22" viewBox="0 0 24 24" fill="none"><circle cx="12" cy="12" r="9" stroke="#60a5fa" stroke-width="1.6" fill="none"/><path d="M12 3v2.5M12 18.5V21M3 12h2.5M18.5 12H21" stroke="#60a5fa" stroke-width="1.4" stroke-linecap="round" opacity="0.5"/><circle cx="12" cy="12" r="3.5" fill="#60a5fa" opacity="0.18"/></svg>',
    tag: 'Privacy-first', wide: true,
  },
  {
    title: 'Global Hotkeys',
    desc: 'Show, hide, or switch modes without ever touching your mouse. Works while any window is focused.',
    icon: '<svg width="22" height="22" viewBox="0 0 24 24" fill="none"><rect x="2" y="5" width="20" height="14" rx="2.5" stroke="#60a5fa" stroke-width="1.6" fill="none"/><path d="M6 9.5h3M15 9.5h3M10 9.5h4M6 13h12" stroke="#60a5fa" stroke-width="1.3" stroke-linecap="round" opacity="0.55"/></svg>',
    tag: null, wide: false,
  },
  {
    title: 'Floating AI Chat',
    desc: 'Pin a resizable chat window anywhere. It floats above all apps, responds in milliseconds, and disappears from every recording.',
    icon: '<svg width="22" height="22" viewBox="0 0 24 24" fill="none"><path d="M3 5h18a1 1 0 011 1v12a1 1 0 01-1 1H6l-4 3V6a1 1 0 011-1z" stroke="#60a5fa" stroke-width="1.6" fill="none"/><path d="M7 10h10M7 14h6" stroke="#60a5fa" stroke-width="1.3" stroke-linecap="round" opacity="0.55"/></svg>',
    tag: null, wide: false,
  },
  {
    title: 'Multi-Model Switching',
    desc: 'Hot-swap between models on the fly. Use a fast model for quick answers, a large model for deep reasoning.',
    icon: '<svg width="22" height="22" viewBox="0 0 24 24" fill="none"><path d="M4 4h6v6H4zM14 4h6v6h-6zM4 14h6v6H4zM14 14h6v6h-6z" stroke="#60a5fa" stroke-width="1.5" fill="none" rx="1"/><path d="M10 7h4M7 10v4M17 10v4M10 17h4" stroke="#60a5fa" stroke-width="1.3" stroke-linecap="round" opacity="0.45"/></svg>',
    tag: 'New', wide: false,
  },
  {
    title: 'Context-Aware Prompts',
    desc: 'GhostlyAI detects what app you\'re in and adjusts its suggestions automatically — coding help in VS Code, answer coaching in Zoom.',
    icon: '<svg width="22" height="22" viewBox="0 0 24 24" fill="none"><path d="M12 2l2.4 7.4H22l-6.2 4.5 2.4 7.4L12 17l-6.2 4.3 2.4-7.4L2 9.4h7.6z" stroke="#60a5fa" stroke-width="1.5" fill="none"/></svg>',
    tag: null, wide: false,
  },
]

const useCases = [
  {
    emoji: '🎯',
    title: 'Technical Interviews',
    badge: 'Most Popular',
    desc: 'GhostlyAI reads the interviewer\'s question on screen and suggests structured answers, hints, and code snippets — all without them seeing a thing.',
  },
  {
    emoji: '💻',
    title: 'Live Coding Help',
    badge: null,
    desc: 'Stuck on a bug mid-call? GhostlyAI reads your editor, identifies the issue, and whispers the fix — instantly, without switching windows.',
  },
  {
    emoji: '📊',
    title: 'Presentation Prep',
    badge: null,
    desc: 'Paste your slides or notes. GhostlyAI gives you speaker notes, stat checks, and counter-arguments — live while you present.',
  },
  {
    emoji: '📄',
    title: 'Document Review',
    badge: null,
    desc: 'Open a contract, report, or research paper. Ask GhostlyAI to summarise, find gaps, or draft a response — without leaving the app.',
  },
  {
    emoji: '🧠',
    title: 'Learning & Research',
    badge: null,
    desc: 'Highlight anything on screen and ask for an explanation. GhostlyAI gives you the depth of a textbook, in seconds.',
  },
  {
    emoji: '🖥️',
    title: 'Desktop Automation',
    badge: 'Coming Soon',
    desc: 'Ask GhostlyAI to complete repetitive tasks — filling forms, summarising emails, moving files — while you focus on what matters.',
  },
]

const steps = [
  {
    icon: '⬇️',
    bg: 'rgba(37,99,235,0.12)',
    title: 'Install Ollama',
    desc: 'Download Ollama from ollama.com and run it. Pull your preferred model with one command.',
    code: 'ollama pull llama3.2',
  },
  {
    icon: '🚀',
    bg: 'rgba(109,40,217,0.12)',
    title: 'Launch GhostlyAI',
    desc: 'Open GhostlyAI — it auto-connects to your Ollama instance. No config, no API keys, no accounts.',
    code: null,
  },
  {
    icon: '👻',
    bg: 'rgba(16,185,129,0.1)',
    title: 'Go invisible',
    desc: 'Press your hotkey, ask anything about what\'s on screen. Get answers instantly. Nobody knows it\'s there.',
    code: null,
  },
]

const privacyPoints = [
  'No data sent to any server',
  'No API keys or accounts',
  'No usage logs or telemetry',
  'Works fully offline',
  'Open source & auditable',
]

const testimonials = [
  {
    quote: 'I landed my dream job at a FAANG company. GhostlyAI helped me stay calm and structured during the technical rounds. Completely invisible on screen share.',
    name: 'Marcus T.',
    role: 'Software Engineer',
    color: 'linear-gradient(135deg, #2563eb, #7c3aed)',
  },
  {
    quote: 'I use it every day for document reviews. I can ask questions about a contract while on a call with a client and they have no idea. It\'s wild.',
    name: 'Priya K.',
    role: 'Legal Consultant',
    color: 'linear-gradient(135deg, #059669, #0284c7)',
  },
  {
    quote: 'The local-only approach is what sold me. I\'m a security researcher — I can\'t send screen data to the cloud. This is the only tool that respects that.',
    name: 'David R.',
    role: 'Security Researcher',
    color: 'linear-gradient(135deg, #d97706, #dc2626)',
  },
]

const faqs = [
  {
    q: 'How does it stay invisible to screen recording software?',
    a: 'GhostlyAI uses platform-specific window APIs — WS_EX_TOOLWINDOW and SetWindowDisplayAffinity on Windows, CGWindowListCopyWindowInfo exclusions on macOS — that tell the OS to omit the window from all capture sources. This is the same technique used by DRM-protected video players.',
  },
  {
    q: 'Which AI models are supported?',
    a: 'Any model available through Ollama: Llama 3.2, Mistral 7B, Gemma 2, DeepSeek Coder, Phi-3, Qwen, and dozens more. You can also switch models on the fly from within the overlay. No cloud model is ever used.',
  },
  {
    q: 'What are the system requirements?',
    a: 'GhostlyAI itself is lightweight. The main requirement is Ollama and your chosen model. For Llama 3.2 3B you need ~4GB RAM; for larger 7B+ models, 8–16GB is recommended. A dedicated GPU speeds things up but is not required.',
  },
  {
    q: 'Is it ethical to use in interviews?',
    a: "That's a fair question. GhostlyAI is a general-purpose desktop productivity tool — no different in principle from having notes open on a second monitor. How you use it is your responsibility. We encourage transparency with interviewers wherever appropriate.",
  },
  {
    q: 'Does it require an internet connection?',
    a: 'No. Everything runs offline. GhostlyAI communicates only with your local Ollama instance. No telemetry, no analytics, no cloud calls — ever.',
  },
  {
    q: 'Will it work on my screen resolution / multi-monitor setup?',
    a: 'Yes. GhostlyAI supports multi-monitor configurations and adapts to any resolution. You can pin the overlay to any monitor independently.',
  },
  {
    q: 'When will it be available to download?',
    a: "We're in active development on both Windows and macOS builds. Sign up above and we'll send you one email the moment it's ready — no spam, no drip campaigns.",
  },
]
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&family=JetBrains+Mono:wght@300;400&display=swap');

html { scroll-behavior: smooth; }
body { font-family: 'Plus Jakarta Sans', sans-serif; -webkit-font-smoothing: antialiased; }

.reveal {
  opacity: 0;
  transform: translateY(18px);
  transition:
    opacity 0.65s cubic-bezier(.22,1,.36,1) var(--d, 0s),
    transform 0.65s cubic-bezier(.22,1,.36,1) var(--d, 0s);
}
.reveal.is-revealed { opacity: 1; transform: translateY(0); }

@keyframes blink {
  0%, 80%, 100% { opacity: 0.18; }
  40% { opacity: 1; }
}
</style>