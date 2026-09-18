# ANIMISH CHOPADE

*Full Stack Developer*

+91-9158067574 · [animishchopade123@gmail.com](mailto:animishchopade123@gmail.com) · [animishchopade.in](https://animishchopade.in) · [linkedin.com/in/animish-chopade](https://linkedin.com/in/animish-chopade) · [github.com/Animish2002](https://github.com/Animish2002)

## PROFESSIONAL SUMMARY

Full Stack Developer with over a year of professional experience building production web applications across modern frontend and backend stacks. Holds a granted patent (2024/03679) for a secure cloud-based document transfer system. Proficient in React, Next.js, Angular, Java/Spring Boot, and Node.js/TypeScript. Hands-on with serverless edge computing (Cloudflare Workers, Hono, D1, R2) — shipping full-stack features end-to-end including payment integrations, AI-powered interfaces, and SaaS design system migrations.

## PROFESSIONAL EXPERIENCE

**Software Developer** — **QNOPY India Private Limited, Pune** *Oct 2025 – Present*

* Migrated the entire legacy UI to a modern SaaS-style project dashboard across four core product modules — Field Flow, Soil Log & Boring Logs, Lab Data, and Atlas (GIS mapping) — building a shared SCSS design system with variables and utility classes that standardised visual consistency across the platform
* Built fully customizable reusable Angular components — dynamic tables, toast notifications, and sidebars — adopted across all product modules, reducing redundant UI code and speeding up development across the team
* Developed RESTful APIs using Spring MVC; managed data persistence with Spring Data JPA / Hibernate and MySQL; applied OOP and SOLID design principles; used Maven for dependency management
* Collaborated in an agile team across the full development lifecycle including code reviews and sprint planning

**Trainee Software Engineer** — **Sciqus Infotech Pvt. Ltd, Pune** *Feb 2024 – Aug 2024*

* Developed Vendor Portal and Export Portal dashboards using React and Tailwind CSS; integrated REST APIs for seamless UI-to-data-layer communication
* Built a reusable component library reducing repetitive code across portals; gained production-level proficiency in React.js, Tailwind CSS, and MySQL

## PROJECTS

[**PrepArena — Competitive Coding Platform**](https://prep-arena.animishchopade.in) | *React 19, TypeScript, Vite, Hono, Cloudflare Workers, D1, KV, R2, Durable Objects, Drizzle ORM, Zustand*

* Built a full-featured LeetCode-style platform with real-time 1v1 battles, friend system with invite-token flow, direct messaging, weekly challenges, spaced repetition revisions, XP/rating system, and a problem library spanning Striver A2Z, Blind 75, and NeetCode 150 sheets across LeetCode, GFG, and CodeChef
* Implemented real-time WebSocket infrastructure via three Cloudflare Durable Objects — BattleRoom (45-min battles with alarm API, per-problem scoring, elapsed-time tie-breaking, async D1 persistence), ChatRoom (persistent DMs with rich message types), and UserFeed (live activity broadcasts to connected clients)
* Built LeetCode account linking with solved-problem sync and a companion browser extension using personal API tokens that auto-marks problems solved in real-time when a LeetCode submission is accepted
* Automated weekly challenges via Cloudflare Cron (every Monday) across 17 DSA topics and 4 formats; implemented spaced repetition scheduling at 1/3/7/15/30-day intervals with per-problem confidence tracking

**Kcal — AI-Powered Calorie Tracker** | *React 19 + React Compiler, TypeScript, Hono, Cloudflare Workers, Gemini 2.0 Flash, D1, R2, Drizzle ORM*

* Built a full-stack calorie tracking PWA with a multi-stage meal logging flow (capture > AI analysis > confirm) — Gemini 2.0 Flash vision analyzes food photos and returns calories, macros, confidence level, and ingredient breakdown, with automatic retry on malformed AI responses and a per-user rate limiter (20 req/hr)
* Designed a provider-agnostic AI abstraction layer (AIProvider interface + factory pattern) allowing zero-route-change swaps between Gemini, OpenAI, or Anthropic; implemented full image lifecycle management — R2 upload with 15-day TTL, daily Cloudflare Cron cleanup at 2am UTC, and JWT auth with PBKDF2/SHA-256 password hashing (100k iterations)
* Built health reporting with 7–90 day macro history, daily summaries, BMI tracking with status labels and AI-generated insights, onboarding flow, and per-user calorie/protein goal tracking; frontend uses React 19 with React Compiler, Zustand, and Framer Motion deployed as a PWA on Cloudflare Pages

**Technical Spark — EdTech SaaS Platform** | *Next.js, React, TypeScript, Hono, Cloudflare Workers, Tailwind CSS, Razorpay, Graphy LMS*

* Built course listing and checkout with dynamic pricing; integrated Razorpay end-to-end (order creation, payment verification, webhooks) and Graphy LMS API for automatic learner enrollment post-payment
* Implemented coupon code system with real-time discount validation; built blog creation and management module; architected the full serverless REST API using Hono on Cloudflare Workers across three deployable services

## TECHNICAL SKILLS

**Languages:** Java, TypeScript, JavaScript, HTML5, CSS3
**Frontend:** React.js, Next.js, Angular, Tailwind CSS, SCSS, RxJS, Zustand, shadcn/ui
**Backend:** Node.js, Express.js, Spring Boot, Hono
**Databases:** PostgreSQL, MySQL, Drizzle ORM
**Cloud & Infra:** Cloudflare Workers, D1, KV, R2, Vercel
**Tools:** Postman, REST Client, Git

## ACHIEVEMENTS

**Granted Patent:** A System for Convenient and Secure Document Transfer to Local Photocopy Centers
**Patent No. 2024/03679** | Granted: December 18, 2024

* Developed a cloud-based document transfer system enabling secure, real-time printing at local photocopy centers, integrating encryption protocols for data security and minimising document leakage risks in public printing facilities

## EDUCATION

**B.Tech — Electronics & Telecommunication Engineering** *CGPA: 8.88 / 10*
BRACT's Vishwakarma Institute of Information Technology, Pune | 2020–2024
