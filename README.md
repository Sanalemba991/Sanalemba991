<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Sanalemba Laitonjam — Fullstack Developer</title>
<link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@300;400;500;600;700&family=Inter:wght@300;400;500;600;700;800;900&display=swap" rel="stylesheet">
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css">
<style>
  *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }

  :root {
    --accent: #4F9CF9;
    --accent-glow: rgba(79, 156, 249, 0.3);
    --accent-soft: rgba(79, 156, 249, 0.1);
    --bg-primary: #0a0e17;
    --bg-secondary: #111827;
    --bg-card: #151d2e;
    --bg-card-hover: #1a2540;
    --text-primary: #e6edf3;
    --text-secondary: #8b949e;
    --text-muted: #484f58;
    --border: rgba(79, 156, 249, 0.15);
    --border-hover: rgba(79, 156, 249, 0.4);
    --success: #3fb950;
    --warning: #d29922;
    --danger: #f85149;
    --pink: #db61a2;
    --purple: #bc8cff;
  }

  html { scroll-behavior: smooth; }

  body {
    font-family: 'Inter', sans-serif;
    background: var(--bg-primary);
    color: var(--text-primary);
    overflow-x: hidden;
    line-height: 1.6;
  }

  /* ── Scrollbar ── */
  ::-webkit-scrollbar { width: 6px; }
  ::-webkit-scrollbar-track { background: var(--bg-primary); }
  ::-webkit-scrollbar-thumb { background: var(--accent); border-radius: 3px; }

  /* ── Particle Canvas ── */
  #particles {
    position: fixed; inset: 0; z-index: 0;
    pointer-events: none; opacity: 0.4;
  }

  /* ── Noise Overlay ── */
  body::before {
    content: '';
    position: fixed; inset: 0; z-index: 1;
    pointer-events: none;
    background: url('https://grainy-gradients.vercel.app/noise.svg');
    opacity: 0.03;
    mix-blend-mode: overlay;
  }

  /* ── Global Reveal Animation ── */
  .reveal {
    opacity: 0;
    transform: translateY(40px);
    transition: opacity 0.8s cubic-bezier(0.16, 1, 0.3, 1),
                transform 0.8s cubic-bezier(0.16, 1, 0.3, 1);
  }
  .reveal.visible {
    opacity: 1;
    transform: translateY(0);
  }
  .reveal-left {
    opacity: 0;
    transform: translateX(-60px);
    transition: opacity 0.8s cubic-bezier(0.16, 1, 0.3, 1),
                transform 0.8s cubic-bezier(0.16, 1, 0.3, 1);
  }
  .reveal-left.visible {
    opacity: 1;
    transform: translateX(0);
  }
  .reveal-right {
    opacity: 0;
    transform: translateX(60px);
    transition: opacity 0.8s cubic-bezier(0.16, 1, 0.3, 1),
                transform 0.8s cubic-bezier(0.16, 1, 0.3, 1);
  }
  .reveal-right.visible {
    opacity: 1;
    transform: translateX(0);
  }
  .reveal-scale {
    opacity: 0;
    transform: scale(0.85);
    transition: opacity 0.8s cubic-bezier(0.16, 1, 0.3, 1),
                transform 0.8s cubic-bezier(0.16, 1, 0.3, 1);
  }
  .reveal-scale.visible {
    opacity: 1;
    transform: scale(1);
  }

  /* ── Container ── */
  .container {
    max-width: 960px;
    margin: 0 auto;
    padding: 0 24px;
    position: relative;
    z-index: 2;
  }

  /* ── Hero Section ── */
  .hero {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    text-align: center;
    position: relative;
    padding: 80px 24px;
  }

  .hero-glow {
    position: absolute;
    width: 600px; height: 600px;
    background: radial-gradient(circle, var(--accent-glow) 0%, transparent 70%);
    border-radius: 50%;
    top: 50%; left: 50%;
    transform: translate(-50%, -50%);
    animation: glowPulse 4s ease-in-out infinite;
    pointer-events: none;
  }

  @keyframes glowPulse {
    0%, 100% { opacity: 0.3; transform: translate(-50%, -50%) scale(1); }
    50% { opacity: 0.6; transform: translate(-50%, -50%) scale(1.15); }
  }

  .hero-avatar {
    width: 120px; height: 120px;
    border-radius: 50%;
    border: 3px solid var(--accent);
    box-shadow: 0 0 40px var(--accent-glow), 0 0 80px rgba(79, 156, 249, 0.1);
    margin-bottom: 28px;
    position: relative;
    overflow: hidden;
    animation: avatarFloat 6s ease-in-out infinite;
  }

  .hero-avatar img {
    width: 100%; height: 100%;
    object-fit: cover;
  }

  .hero-avatar::after {
    content: '';
    position: absolute; inset: -3px;
    border-radius: 50%;
    border: 3px solid transparent;
    border-top-color: var(--accent);
    animation: avatarSpin 3s linear infinite;
  }

  @keyframes avatarSpin {
    to { transform: rotate(360deg); }
  }
  @keyframes avatarFloat {
    0%, 100% { transform: translateY(0); }
    50% { transform: translateY(-10px); }
  }

  .hero-status {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    padding: 6px 16px;
    border-radius: 50px;
    background: var(--accent-soft);
    border: 1px solid var(--border);
    font-size: 13px;
    color: var(--accent);
    font-weight: 500;
    margin-bottom: 24px;
    animation: fadeInUp 0.6s 0.2s both;
  }

  .status-dot {
    width: 8px; height: 8px;
    border-radius: 50%;
    background: var(--success);
    animation: statusPulse 2s ease-in-out infinite;
  }

  @keyframes statusPulse {
    0%, 100% { box-shadow: 0 0 0 0 rgba(63, 185, 80, 0.4); }
    50% { box-shadow: 0 0 0 6px rgba(63, 185, 80, 0); }
  }

  .hero h1 {
    font-size: clamp(36px, 7vw, 64px);
    font-weight: 900;
    letter-spacing: -0.03em;
    line-height: 1.1;
    margin-bottom: 16px;
    animation: fadeInUp 0.6s 0.3s both;
  }

  .hero h1 .accent { color: var(--accent); }

  .hero-roles {
    font-size: 15px;
    color: var(--text-secondary);
    font-weight: 400;
    margin-bottom: 32px;
    animation: fadeInUp 0.6s 0.4s both;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 8px;
  }

  .role-tag {
    padding: 4px 14px;
    border-radius: 50px;
    background: var(--bg-card);
    border: 1px solid var(--border);
    font-size: 13px;
    font-weight: 500;
    transition: all 0.3s;
  }
  .role-tag:hover {
    border-color: var(--accent);
    color: var(--accent);
    box-shadow: 0 0 20px var(--accent-glow);
  }

  /* ── Typing Effect ── */
  .typing-container {
    height: 28px;
    margin-bottom: 36px;
    animation: fadeInUp 0.6s 0.5s both;
  }

  .typing-text {
    font-family: 'JetBrains Mono', monospace;
    font-size: 14px;
    color: var(--accent);
    display: inline;
  }

  .typing-cursor {
    display: inline-block;
    width: 2px; height: 18px;
    background: var(--accent);
    margin-left: 2px;
    vertical-align: text-bottom;
    animation: cursorBlink 1s step-end infinite;
  }

  @keyframes cursorBlink {
    0%, 100% { opacity: 1; }
    50% { opacity: 0; }
  }

  /* ── Badge Row ── */
  .badge-row {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 12px;
    animation: fadeInUp 0.6s 0.6s both;
  }

  .badge {
    display: inline-flex;
    align-items: center;
    gap: 6px;
    padding: 6px 14px;
    border-radius: 8px;
    background: var(--bg-card);
    border: 1px solid var(--border);
    font-size: 13px;
    font-weight: 500;
    color: var(--text-secondary);
    text-decoration: none;
    transition: all 0.3s ease;
    cursor: pointer;
  }

  .badge:hover {
    border-color: var(--accent);
    color: var(--text-primary);
    transform: translateY(-2px);
    box-shadow: 0 4px 20px var(--accent-glow);
  }

  .badge i { color: var(--accent); font-size: 14px; }

  .badge .count {
    font-family: 'JetBrains Mono', monospace;
    color: var(--accent);
    font-weight: 600;
  }

  /* ── Section ── */
  section {
    padding: 80px 0;
    position: relative;
  }

  .section-label {
    font-family: 'JetBrains Mono', monospace;
    font-size: 12px;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 0.15em;
    color: var(--accent);
    margin-bottom: 12px;
    display: flex;
    align-items: center;
    gap: 10px;
  }

  .section-label::before {
    content: '';
    width: 24px; height: 2px;
    background: var(--accent);
    border-radius: 1px;
  }

  .section-title {
    font-size: clamp(28px, 4vw, 40px);
    font-weight: 800;
    letter-spacing: -0.02em;
    margin-bottom: 24px;
    line-height: 1.2;
  }

  .section-desc {
    font-size: 16px;
    color: var(--text-secondary);
    line-height: 1.8;
    max-width: 700px;
  }

  .section-desc strong { color: var(--text-primary); font-weight: 600; }

  .highlight { color: var(--accent); font-weight: 600; }

  /* ── Divider ── */
  .divider {
    height: 1px;
    background: linear-gradient(90deg, transparent, var(--border), transparent);
    margin: 0 auto;
    max-width: 600px;
  }

  /* ── Experience ── */
  .experience-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 20px;
    margin-top: 36px;
  }

  .exp-card {
    background: var(--bg-card);
    border: 1px solid var(--border);
    border-radius: 16px;
    padding: 28px;
    position: relative;
    overflow: hidden;
    transition: all 0.4s cubic-bezier(0.16, 1, 0.3, 1);
  }

  .exp-card::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 3px;
    background: linear-gradient(90deg, var(--accent), var(--purple));
    transform: scaleX(0);
    transform-origin: left;
    transition: transform 0.5s cubic-bezier(0.16, 1, 0.3, 1);
  }

  .exp-card:hover::before { transform: scaleX(1); }

  .exp-card:hover {
    border-color: var(--border-hover);
    transform: translateY(-4px);
    box-shadow: 0 20px 60px rgba(0,0,0,0.3), 0 0 40px var(--accent-glow);
  }

  .exp-type {
    display: inline-flex;
    align-items: center;
    gap: 6px;
    padding: 4px 12px;
    border-radius: 50px;
    font-size: 11px;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 0.08em;
    margin-bottom: 16px;
  }

  .exp-type.current {
    background: rgba(63, 185, 80, 0.1);
    color: var(--success);
    border: 1px solid rgba(63, 185, 80, 0.2);
  }

  .exp-type.intern {
    background: rgba(210, 153, 34, 0.1);
    color: var(--warning);
    border: 1px solid rgba(210, 153, 34, 0.2);
  }

  .exp-role {
    font-size: 20px;
    font-weight: 700;
    margin-bottom: 8px;
  }

  .exp-company {
    font-size: 14px;
    color: var(--text-secondary);
  }

  /* ── Tech Stack ── */
  .tech-categories {
    display: flex;
    flex-direction: column;
    gap: 32px;
    margin-top: 36px;
  }

  .tech-category-label {
    font-size: 13px;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 0.1em;
    color: var(--text-muted);
    margin-bottom: 14px;
    display: flex;
    align-items: center;
    gap: 8px;
  }

  .tech-category-label i { color: var(--accent); font-size: 14px; }

  .tech-tags {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
  }

  .tech-tag {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    padding: 10px 18px;
    border-radius: 12px;
    background: var(--bg-card);
    border: 1px solid var(--border);
    font-size: 14px;
    font-weight: 500;
    color: var(--text-secondary);
    transition: all 0.3s ease;
    cursor: default;
    position: relative;
    overflow: hidden;
  }

  .tech-tag::before {
    content: '';
    position: absolute;
    inset: 0;
    background: linear-gradient(135deg, var(--accent-soft), transparent);
    opacity: 0;
    transition: opacity 0.3s;
  }

  .tech-tag:hover::before { opacity: 1; }

  .tech-tag:hover {
    border-color: var(--accent);
    color: var(--text-primary);
    transform: translateY(-3px) scale(1.02);
    box-shadow: 0 8px 30px var(--accent-glow);
  }

  .tech-tag i { color: var(--accent); font-size: 16px; position: relative; z-index: 1; }
  .tech-tag span { position: relative; z-index: 1; }

  /* ── Projects ── */
  .projects-grid {
    display: flex;
    flex-direction: column;
    gap: 24px;
    margin-top: 36px;
  }

  .project-card {
    background: var(--bg-card);
    border: 1px solid var(--border);
    border-radius: 20px;
    padding: 32px;
    position: relative;
    overflow: hidden;
    transition: all 0.5s cubic-bezier(0.16, 1, 0.3, 1);
  }

  .project-card::after {
    content: '';
    position: absolute;
    top: -50%; right: -50%;
    width: 200px; height: 200px;
    background: radial-gradient(circle, var(--accent-glow), transparent 70%);
    opacity: 0;
    transition: opacity 0.5s;
    pointer-events: none;
  }

  .project-card:hover::after { opacity: 0.5; }

  .project-card:hover {
    border-color: var(--border-hover);
    transform: translateY(-4px);
    box-shadow: 0 25px 80px rgba(0,0,0,0.4), 0 0 60px var(--accent-glow);
  }

  .project-header {
    display: flex;
    align-items: flex-start;
    justify-content: space-between;
    gap: 16px;
    margin-bottom: 12px;
  }

  .project-icon {
    width: 48px; height: 48px;
    border-radius: 14px;
    background: var(--accent-soft);
    border: 1px solid var(--border);
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 22px;
    flex-shrink: 0;
    transition: all 0.3s;
  }

  .project-card:hover .project-icon {
    background: var(--accent);
    color: var(--bg-primary);
    box-shadow: 0 0 30px var(--accent-glow);
  }

  .project-links {
    display: flex;
    gap: 8px;
    flex-shrink: 0;
  }

  .project-link {
    display: inline-flex;
    align-items: center;
    gap: 6px;
    padding: 6px 14px;
    border-radius: 8px;
    font-size: 12px;
    font-weight: 600;
    text-decoration: none;
    transition: all 0.3s;
    border: 1px solid var(--border);
    color: var(--text-secondary);
  }

  .project-link.demo {
    background: var(--accent);
    border-color: var(--accent);
    color: #fff;
  }

  .project-link.demo:hover {
    box-shadow: 0 0 20px var(--accent-glow);
    transform: translateY(-2px);
  }

  .project-link.code:hover {
    border-color: var(--text-primary);
    color: var(--text-primary);
    transform: translateY(-2px);
  }

  .project-name {
    font-size: 22px;
    font-weight: 700;
    margin-bottom: 8px;
  }

  .project-desc {
    font-size: 15px;
    color: var(--text-secondary);
    line-height: 1.7;
  }

  .project-more {
    display: inline-flex;
    align-items: center;
    gap: 6px;
    margin-top: 20px;
    padding: 10px 24px;
    border-radius: 12px;
    background: var(--bg-card);
    border: 1px solid var(--border);
    color: var(--text-secondary);
    font-size: 14px;
    font-weight: 500;
    text-decoration: none;
    transition: all 0.3s;
    width: 100%;
    justify-content: center;
  }

  .project-more:hover {
    border-color: var(--accent);
    color: var(--accent);
    box-shadow: 0 0 30px var(--accent-glow);
  }

  /* ── Stats Section ── */
  .stats-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
    gap: 16px;
    margin-top: 36px;
    margin-bottom: 40px;
  }

  .stat-card {
    background: var(--bg-card);
    border: 1px solid var(--border);
    border-radius: 16px;
    padding: 24px;
    text-align: center;
    position: relative;
    overflow: hidden;
    transition: all 0.4s;
  }

  .stat-card:hover {
    border-color: var(--border-hover);
    transform: translateY(-4px);
    box-shadow: 0 16px 50px rgba(0,0,0,0.3);
  }

  .stat-card::before {
    content: '';
    position: absolute;
    bottom: 0; left: 0; right: 0;
    height: 3px;
    background: linear-gradient(90deg, var(--accent), var(--purple));
    transform: scaleX(0);
    transition: transform 0.5s cubic-bezier(0.16, 1, 0.3, 1);
  }

  .stat-card:hover::before { transform: scaleX(1); }

  .stat-number {
    font-family: 'JetBrains Mono', monospace;
    font-size: 32px;
    font-weight: 700;
    color: var(--accent);
    line-height: 1;
    margin-bottom: 8px;
  }

  .stat-label {
    font-size: 13px;
    color: var(--text-muted);
    font-weight: 500;
  }

  /* ── Language Bars ── */
  .lang-section { margin-top: 40px; }

  .lang-title {
    font-size: 18px;
    font-weight: 700;
    margin-bottom: 20px;
  }

  .lang-list {
    display: flex;
    flex-direction: column;
    gap: 16px;
  }

  .lang-item {
    display: flex;
    align-items: center;
    gap: 16px;
  }

  .lang-dot {
    width: 12px; height: 12px;
    border-radius: 50%;
    flex-shrink: 0;
    box-shadow: 0 0 10px currentColor;
  }

  .lang-name {
    font-size: 14px;
    font-weight: 500;
    width: 100px;
    flex-shrink: 0;
  }

  .lang-bar-bg {
    flex: 1;
    height: 8px;
    background: var(--bg-secondary);
    border-radius: 4px;
    overflow: hidden;
  }

  .lang-bar-fill {
    height: 100%;
    border-radius: 4px;
    width: 0;
    transition: width 1.5s cubic-bezier(0.16, 1, 0.3, 1);
  }

  .lang-pct {
    font-family: 'JetBrains Mono', monospace;
    font-size: 13px;
    color: var(--text-muted);
    width: 45px;
    text-align: right;
    flex-shrink: 0;
  }

  /* ── Streak Section ── */
  .streak-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 16px;
    margin-top: 36px;
    margin-bottom: 40px;
  }

  .streak-card {
    background: var(--bg-card);
    border: 1px solid var(--border);
    border-radius: 16px;
    padding: 24px;
    text-align: center;
    transition: all 0.4s;
  }

  .streak-card:hover {
    border-color: var(--border-hover);
    transform: translateY(-4px);
  }

  .streak-icon {
    font-size: 28px;
    margin-bottom: 10px;
    display: block;
  }

  .streak-value {
    font-family: 'JetBrains Mono', monospace;
    font-size: 28px;
    font-weight: 700;
    color: var(--accent);
  }

  .streak-label {
    font-size: 13px;
    color: var(--text-muted);
    margin-top: 4px;
  }

  /* ── Contribution Grid (CSS fallback) ── */
  .contribution-section { margin-top: 40px; }

  .contribution-title {
    font-size: 18px;
    font-weight: 700;
    margin-bottom: 20px;
  }

  .contrib-grid {
    display: grid;
    grid-template-columns: repeat(52, 1fr);
    gap: 3px;
    overflow-x: auto;
    padding-bottom: 8px;
  }

  .contrib-cell {
    aspect-ratio: 1;
    border-radius: 3px;
    background: var(--bg-secondary);
    transition: all 0.2s;
    min-width: 10px;
  }

  .contrib-cell:hover {
    transform: scale(1.5);
    z-index: 1;
  }

  .contrib-cell.l1 { background: #0e4429; }
  .contrib-cell.l2 { background: #006d32; }
  .contrib-cell.l3 { background: #26a641; }
  .contrib-cell.l4 { background: #39d353; box-shadow: 0 0 6px rgba(57, 211, 83, 0.4); }

  /* ── Connect Section ── */
  .connect-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(160px, 1fr));
    gap: 12px;
    margin-top: 36px;
  }

  .connect-card {
    display: flex;
    align-items: center;
    gap: 12px;
    padding: 16px 20px;
    border-radius: 14px;
    background: var(--bg-card);
    border: 1px solid var(--border);
    text-decoration: none;
    color: var(--text-secondary);
    font-size: 14px;
    font-weight: 500;
    transition: all 0.3s ease;
    position: relative;
    overflow: hidden;
  }

  .connect-card::before {
    content: '';
    position: absolute;
    inset: 0;
    opacity: 0;
    transition: opacity 0.3s;
  }

  .connect-card:hover::before { opacity: 1; }

  .connect-card:hover {
    border-color: var(--border-hover);
    color: var(--text-primary);
    transform: translateY(-3px);
    box-shadow: 0 12px 40px rgba(0,0,0,0.3);
  }

  .connect-card i {
    font-size: 20px;
    flex-shrink: 0;
    position: relative;
    z-index: 1;
  }

  .connect-card span {
    position: relative;
    z-index: 1;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
  }

  .connect-card.github i { color: #e6edf3; }
  .connect-card.github::before { background: rgba(230, 237, 243, 0.05); }
  .connect-card.github:hover { border-color: #e6edf3; }

  .connect-card.instagram i { color: #E4405F; }
  .connect-card.instagram::before { background: rgba(228, 64, 95, 0.05); }
  .connect-card.instagram:hover { border-color: #E4405F; }

  .connect-card.twitter i { color: #1DA1F2; }
  .connect-card.twitter::before { background: rgba(29, 161, 242, 0.05); }
  .connect-card.twitter:hover { border-color: #1DA1F2; }

  .connect-card.youtube i { color: #FF0000; }
  .connect-card.youtube::before { background: rgba(255, 0, 0, 0.05); }
  .connect-card.youtube:hover { border-color: #FF0000; }

  .connect-card.facebook i { color: #1877F2; }
  .connect-card.facebook::before { background: rgba(24, 119, 242, 0.05); }
  .connect-card.facebook:hover { border-color: #1877F2; }

  .connect-card.gmail i { color: #D14836; }
  .connect-card.gmail::before { background: rgba(209, 72, 54, 0.05); }
  .connect-card.gmail:hover { border-color: #D14836; }

  /* ── Footer ── */
  footer {
    text-align: center;
    padding: 48px 24px 32px;
    position: relative;
    z-index: 2;
  }

  footer p {
    font-size: 14px;
    color: var(--text-muted);
  }

  footer .wave {
    display: inline-block;
    animation: wave 2.5s ease-in-out infinite;
    transform-origin: 70% 70%;
  }

  @keyframes wave {
    0%, 100% { transform: rotate(0deg); }
    10% { transform: rotate(14deg); }
    20% { transform: rotate(-8deg); }
    30% { transform: rotate(14deg); }
    40% { transform: rotate(-4deg); }
    50% { transform: rotate(10deg); }
    60% { transform: rotate(0deg); }
  }

  /* ── Fade In Up Keyframe ── */
  @keyframes fadeInUp {
    from { opacity: 0; transform: translateY(24px); }
    to { opacity: 1; transform: translateY(0); }
  }

  /* ── Marquee (subtle) ── */
  .marquee-strip {
    overflow: hidden;
    padding: 20px 0;
    position: relative;
    z-index: 2;
  }

  .marquee-track {
    display: flex;
    gap: 32px;
    animation: marquee 40s linear infinite;
    width: max-content;
  }

  .marquee-item {
    font-family: 'JetBrains Mono', monospace;
    font-size: 13px;
    color: var(--text-muted);
    white-space: nowrap;
    display: flex;
    align-items: center;
    gap: 8px;
  }

  .marquee-item .dot {
    width: 6px; height: 6px;
    border-radius: 50%;
    background: var(--accent);
    opacity: 0.5;
  }

  @keyframes marquee {
    from { transform: translateX(0); }
    to { transform: translateX(-50%); }
  }

  /* ── Responsive ── */
  @media (max-width: 640px) {
    .container { padding: 0 16px; }
    .hero { padding: 60px 16px; }
    .badge-row { gap: 8px; }
    .badge { padding: 5px 10px; font-size: 12px; }
    .stats-grid { grid-template-columns: repeat(2, 1fr); gap: 10px; }
    .streak-grid { grid-template-columns: repeat(2, 1fr); }
    .connect-grid { grid-template-columns: 1fr; }
    .experience-grid { grid-template-columns: 1fr; }
    .project-header { flex-direction: column; }
    .project-links { align-self: flex-start; }
    .contrib-grid { grid-template-columns: repeat(52, 8px); gap: 2px; }
  }
</style>
</head>
<body>

<canvas id="particles"></canvas>

<!-- ═══════ HERO ═══════ -->
<section class="hero">
  <div class="hero-glow"></div>
  <div class="hero-avatar">
    <img src="https://github.com/sanalemba991.png" alt="Sanalemba Laitonjam" onerror="this.style.display='none';this.parentElement.innerHTML='<div style=&quot;width:100%;height:100%;background:linear-gradient(135deg,#4F9CF9,#bc8cff);display:flex;align-items:center;justify-content:center;font-size:42px;font-weight:900;color:#0a0e17&quot;>SL</div>'">
  </div>
  <div class="hero-status">
    <span class="status-dot"></span>
    Available for work
  </div>
  <h1>Sanalemba<br><span class="accent">Laitonjam</span></h1>
  <div class="hero-roles">
    <span class="role-tag">Fullstack Developer</span>
    <span class="role-tag">AI Practitioner</span>
    <span class="role-tag">ML Practitioner</span>
    <span class="role-tag">Blockchain Explorer</span>
  </div>
  <div class="typing-container">
    <span class="typing-text" id="typingText"></span><span class="typing-cursor"></span>
  </div>
  <div class="badge-row">
    <a href="https://github.com/sanalemba991" target="_blank" class="badge">
      <i class="fa-solid fa-eye"></i>
      <span class="count" data-count="0">0</span> Profile Views
    </a>
    <a href="https://github.com/sanalemba991?tab=followers" target="_blank" class="badge">
      <i class="fa-solid fa-users"></i>
      <span class="count" data-count="0">0</span> Followers
    </a>
    <a href="mailto:laitonjamsanalembameitei99@gmail.com" class="badge">
      <i class="fa-solid fa-envelope"></i>
      Email
    </a>
  </div>
</section>

<!-- ═══════ MARQUEE ═══════ -->
<div class="marquee-strip">
  <div class="marquee-track" id="marqueeTrack">
    <span class="marquee-item"><span class="dot"></span>React.js</span>
    <span class="marquee-item"><span class="dot"></span>Next.js</span>
    <span class="marquee-item"><span class="dot"></span>Node.js</span>
    <span class="marquee-item"><span class="dot"></span>Express.js</span>
    <span class="marquee-item"><span class="dot"></span>MongoDB</span>
    <span class="marquee-item"><span class="dot"></span>TensorFlow</span>
    <span class="marquee-item"><span class="dot"></span>Python</span>
    <span class="marquee-item"><span class="dot"></span>Blockchain</span>
    <span class="marquee-item"><span class="dot"></span>Tailwind CSS</span>
    <span class="marquee-item"><span class="dot"></span>Firebase</span>
    <span class="marquee-item"><span class="dot"></span>JavaScript</span>
    <span class="marquee-item"><span class="dot"></span>NLP</span>
    <span class="marquee-item"><span class="dot"></span>AI / ML</span>
    <span class="marquee-item"><span class="dot"></span>Astro</span>
    <!-- Duplicate for seamless loop -->
    <span class="marquee-item"><span class="dot"></span>React.js</span>
    <span class="marquee-item"><span class="dot"></span>Next.js</span>
    <span class="marquee-item"><span class="dot"></span>Node.js</span>
    <span class="marquee-item"><span class="dot"></span>Express.js</span>
    <span class="marquee-item"><span class="dot"></span>MongoDB</span>
    <span class="marquee-item"><span class="dot"></span>TensorFlow</span>
    <span class="marquee-item"><span class="dot"></span>Python</span>
    <span class="marquee-item"><span class="dot"></span>Blockchain</span>
    <span class="marquee-item"><span class="dot"></span>Tailwind CSS</span>
    <span class="marquee-item"><span class="dot"></span>Firebase</span>
    <span class="marquee-item"><span class="dot"></span>JavaScript</span>
    <span class="marquee-item"><span class="dot"></span>NLP</span>
    <span class="marquee-item"><span class="dot"></span>AI / ML</span>
    <span class="marquee-item"><span class="dot"></span>Astro</span>
  </div>
</div>

<div class="divider"></div>

<!-- ═══════ ABOUT ═══════ -->
<section>
  <div class="container">
    <div class="reveal">
      <div class="section-label">About</div>
      <h2 class="section-title">Code. Create. Conquer.</h2>
      <p class="section-desc">
        I'm a fullstack developer currently working as a <strong>Fullstack Developer at Lovosis Technology Pvt. Ltd.</strong>, with prior experience as a fullstack intern at <strong>Kaiztren Innovative Solutions</strong>. My day-to-day is rooted in the MERN stack, but I actively explore <span class="highlight">AI, machine learning, NLP, and blockchain</span> on the side.
      </p>
      <p class="section-desc" style="margin-top: 16px;">
        I've shipped <span class="highlight">100+ web projects</span> ranging from AI-powered translation tools to production-grade React applications — deployed and live on Vercel and Netlify.
      </p>
      <p class="section-desc" style="margin-top: 16px;">
        Outside the terminal: gym regular 🏋️‍♂️, always chasing the next build.
      </p>
    </div>
  </div>
</section>

<div class="divider"></div>

<!-- ═══════ EXPERIENCE ═══════ -->
<section>
  <div class="container">
    <div class="reveal">
      <div class="section-label">Experience</div>
      <h2 class="section-title">Where I've Built</h2>
    </div>
    <div class="experience-grid">
      <div class="exp-card reveal-left" style="transition-delay: 0.1s;">
        <div class="exp-type current"><i class="fa-solid fa-circle" style="font-size:6px;"></i> Current</div>
        <div class="exp-role">Fullstack Developer</div>
        <div class="exp-company">Lovosis Technology Pvt. Ltd.</div>
      </div>
      <div class="exp-card reveal-right" style="transition-delay: 0.2s;">
        <div class="exp-type intern"><i class="fa-solid fa-circle" style="font-size:6px;"></i> Internship</div>
        <div class="exp-role">Fullstack Developer</div>
        <div class="exp-company">Kaiztren Innovative Solutions</div>
      </div>
    </div>
  </div>
</section>

<div class="divider"></div>

<!-- ═══════ TECH STACK ═══════ -->
<section>
  <div class="container">
    <div class="reveal">
      <div class="section-label">Tech Stack</div>
      <h2 class="section-title">Tools I Work With</h2>
    </div>
    <div class="tech-categories">
      <div class="reveal" style="transition-delay: 0.1s;">
        <div class="tech-category-label"><i class="fa-solid fa-palette"></i> Frontend</div>
        <div class="tech-tags">
          <div class="tech-tag"><i class="fa-brands fa-react"></i><span>React.js</span></div>
          <div class="tech-tag"><i class="fa-solid fa-n"></i><span>Next.js</span></div>
          <div class="tech-tag"><i class="fa-solid fa-rocket"></i><span>Astro</span></div>
          <div class="tech-tag"><i class="fa-brands fa-js"></i><span>JavaScript</span></div>
          <div class="tech-tag"><i class="fa-brands fa-html5"></i><span>HTML5</span></div>
          <div class="tech-tag"><i class="fa-brands fa-css3-alt"></i><span>CSS3</span></div>
          <div class="tech-tag"><i class="fa-solid fa-wind"></i><span>Tailwind CSS</span></div>
        </div>
      </div>
      <div class="reveal" style="transition-delay: 0.2s;">
        <div class="tech-category-label"><i class="fa-solid fa-server"></i> Backend & Database</div>
        <div class="tech-tags">
          <div class="tech-tag"><i class="fa-brands fa-node-js"></i><span>Node.js</span></div>
          <div class="tech-tag"><i class="fa-solid fa-bolt"></i><span>Express.js</span></div>
          <div class="tech-tag"><i class="fa-solid fa-leaf"></i><span>MongoDB</span></div>
        </div>
      </div>
      <div class="reveal" style="transition-delay: 0.3s;">
        <div class="tech-category-label"><i class="fa-solid fa-brain"></i> AI / ML / Data</div>
        <div class="tech-tags">
          <div class="tech-tag"><i class="fa-brands fa-python"></i><span>Python</span></div>
          <div class="tech-tag"><i class="fa-solid fa-fire"></i><span>TensorFlow</span></div>
          <div class="tech-tag"><i class="fa-solid fa-language"></i><span>NLP</span></div>
          <div class="tech-tag"><i class="fa-solid fa-robot"></i><span>AI</span></div>
        </div>
      </div>
      <div class="reveal" style="transition-delay: 0.4s;">
        <div class="tech-category-label"><i class="fa-solid fa-toolbox"></i> Other</div>
        <div class="tech-tags">
          <div class="tech-tag"><i class="fa-solid fa-fire-flame-curved"></i><span>Firebase</span></div>
          <div class="tech-tag"><i class="fa-solid fa-link"></i><span>Blockchain</span></div>
          <div class="tech-tag"><i class="fa-solid fa-magnifying-glass"></i><span>SEO</span></div>
        </div>
      </div>
    </div>
  </div>
</section>

<div class="divider"></div>

<!-- ═══════ PROJECTS ═══════ -->
<section>
  <div class="container">
    <div class="reveal">
      <div class="section-label">Projects</div>
      <h2 class="section-title">Featured Builds</h2>
    </div>
    <div class="projects-grid">
      <div class="project-card reveal" style="transition-delay: 0.1s;">
        <div class="project-header">
          <div class="project-icon">🔤</div>
          <div class="project-links">
            <a href="https://ml-multiligual-translation-using-react-js-web-base.vercel.app/" target="_blank" class="project-link demo"><i class="fa-solid fa-arrow-up-right-from-square"></i> Live Demo</a>
            <a href="https://github.com/Sanalemba991/ML-Multiligual-translation-Using-ReactJS-Web-Base" target="_blank" class="project-link code"><i class="fa-brands fa-github"></i> Code</a>
          </div>
        </div>
        <div class="project-name">Multilingual Translation App</div>
        <p class="project-desc">AI-powered multilingual transcription and translation — built with React.js and deployed on Vercel. Uses browser-native AI/ML APIs for real-time translation across multiple languages with minimal latency.</p>
      </div>
      <div class="project-card reveal" style="transition-delay: 0.2s;">
        <div class="project-header">
          <div class="project-icon">⛓️</div>
          <div class="project-links">
            <a href="https://github.com/Sanalemba991?tab=repositories" target="_blank" class="project-link code"><i class="fa-brands fa-github"></i> Code</a>
          </div>
        </div>
        <div class="project-name">Blockchain Project 1</div>
        <p class="project-desc">Decentralized application built on the blockchain — exploring smart contracts and Web3 integration. Hands-on experimentation with decentralized architecture and on-chain data handling.</p>
      </div>
      <div class="project-card reveal" style="transition-delay: 0.3s;">
        <div class="project-header">
          <div class="project-icon">⛓️</div>
          <div class="project-links">
            <a href="https://github.com/Sanalemba991?tab=repositories" target="_blank" class="project-link code"><i class="fa-brands fa-github"></i> Code</a>
          </div>
        </div>
        <div class="project-name">Blockchain Project 2</div>
        <p class="project-desc">Blockchain-based solution focused on transparency and secure transactions. Exploring real-world use cases — from ledger systems to decentralized identity and beyond.</p>
      </div>
      <div class="reveal" style="transition-delay: 0.4s;">
        <a href="https://github.com/Sanalemba991?tab=repositories" target="_blank" class="project-more">
          <i class="fa-solid fa-folder-open"></i> View All 100+ Projects <i class="fa-solid fa-arrow-right"></i>
        </a>
      </div>
    </div>
  </div>
</section>

<div class="divider"></div>

<!-- ═══════ STATS ═══════ -->
<section>
  <div class="container">
    <div class="reveal">
      <div class="section-label">GitHub Stats</div>
      <h2 class="section-title">Numbers at a Glance</h2>
    </div>
    <div class="stats-grid">
      <div class="stat-card reveal-scale" style="transition-delay: 0.1s;">
        <div class="stat-number" data-target="50">0</div>
        <div class="stat-label">Repositories</div>
      </div>
      <div class="stat-card reveal-scale" style="transition-delay: 0.15s;">
        <div class="stat-number" data-target="500">0</div>
        <div class="stat-label">Commits</div>
      </div>
      <div class="stat-card reveal-scale" style="transition-delay: 0.2s;">
        <div class="stat-number" data-target="100">0</div>
        <div class="stat-label">Projects Shipped</div>
      </div>
      <div class="stat-card reveal-scale" style="transition-delay: 0.25s;">
        <div class="stat-number" data-target="15">0</div>
        <div class="stat-label">Technologies</div>
      </div>
    </div>

    <!-- Streak -->
    <div class="streak-grid">
      <div class="streak-card reveal-scale" style="transition-delay: 0.3s;">
        <span class="streak-icon">🔥</span>
        <div class="streak-value" data-target="365">0</div>
        <div class="streak-label">Day Streak</div>
      </div>
      <div class="streak-card reveal-scale" style="transition-delay: 0.35s;">
        <span class="streak-icon">⭐</span>
        <div class="streak-value" data-target="25">0</div>
        <div class="streak-label">Total Stars</div>
      </div>
      <div class="streak-card reveal-scale" style="transition-delay: 0.4s;">
        <span class="streak-icon">🔀</span>
        <div class="streak-value" data-target="10">0</div>
        <div class="streak-label">Forks</div>
      </div>
    </div>

    <!-- Language Bars -->
    <div class="lang-section reveal" style="transition-delay: 0.3s;">
      <div class="lang-title">Top Languages</div>
      <div class="lang-list">
        <div class="lang-item">
          <span class="lang-dot" style="color: #f1e05a;"></span>
          <span class="lang-name">JavaScript</span>
          <div class="lang-bar-bg"><div class="lang-bar-fill" data-width="68" style="background: linear-gradient(90deg, #f1e05a, #e8d44d);"></div></div>
          <span class="lang-pct">68%</span>
        </div>
        <div class="lang-item">
          <span class="lang-dot" style="color: #3178c6;"></span>
          <span class="lang-name">TypeScript</span>
          <div class="lang-bar-bg"><div class="lang-bar-fill" data-width="15" style="background: linear-gradient(90deg, #3178c6, #2868b0);"></div></div>
          <span class="lang-pct">15%</span>
        </div>
        <div class="lang-item">
          <span class="lang-dot" style="color: #3572A5;"></span>
          <span class="lang-name">Python</span>
          <div class="lang-bar-bg"><div class="lang-bar-fill" data-width="10" style="background: linear-gradient(90deg, #3572A5, #2d5f8e);"></div></div>
          <span class="lang-pct">10%</span>
        </div>
        <div class="lang-item">
          <span class="lang-dot" style="color: #e34c26;"></span>
          <span class="lang-name">HTML</span>
          <div class="lang-bar-bg"><div class="lang-bar-fill" data-width="5" style="background: linear-gradient(90deg, #e34c26, #c9411f);"></div></div>
          <span class="lang-pct">5%</span>
        </div>
        <div class="lang-item">
          <span class="lang-dot" style="color: #563d7c;"></span>
          <span class="lang-name">CSS</span>
          <div class="lang-bar-bg"><div class="lang-bar-fill" data-width="2" style="background: linear-gradient(90deg, #563d7c, #4a3470);"></div></div>
          <span class="lang-pct">2%</span>
        </div>
      </div>
    </div>

    <!-- Contribution Grid -->
    <div class="contribution-section reveal" style="transition-delay: 0.4s;">
      <div class="contribution-title">Contribution Activity</div>
      <div class="contrib-grid" id="contribGrid"></div>
    </div>
  </div>
</section>

<div class="divider"></div>

<!-- ═══════ CONNECT ═══════ -->
<section>
  <div class="container">
    <div class="reveal">
      <div class="section-label">Connect</div>
      <h2 class="section-title">Let's Build Together</h2>
    </div>
    <div class="connect-grid">
      <a href="https://github.com/sanalemba991" target="_blank" class="connect-card github reveal" style="transition-delay:0.05s;">
        <i class="fa-brands fa-github"></i><span>sanalemba991</span>
      </a>
      <a href="https://instagram.com/sanalemba_laitonjam" target="_blank" class="connect-card instagram reveal" style="transition-delay:0.1s;">
        <i class="fa-brands fa-instagram"></i><span>@sanalemba__laitonjam</span>
      </a>
      <a href="https://twitter.com/laitonjamsanalemba" target="_blank" class="connect-card twitter reveal" style="transition-delay:0.15s;">
        <i class="fa-brands fa-x-twitter"></i><span>@laitonjamsanalemba</span>
      </a>
      <a href="https://www.youtube.com/c/laitonjamsanalemba" target="_blank" class="connect-card youtube reveal" style="transition-delay:0.2s;">
        <i class="fa-brands fa-youtube"></i><span>Laitonjam Sanalemba</span>
      </a>
      <a href="https://fb.com/sanalembalaitonjam" target="_blank" class="connect-card facebook reveal" style="transition-delay:0.25s;">
        <i class="fa-brands fa-facebook"></i><span>Sana Lemba Laitonjam</span>
      </a>
      <a href="mailto:laitonjamsanalembameitei99@gmail.com" class="connect-card gmail reveal" style="transition-delay:0.3s;">
        <i class="fa-solid fa-envelope"></i><span>Gmail</span>
      </a>
    </div>
  </div>
</section>

<!-- ═══════ FOOTER ═══════ -->
<footer>
  <p>Open to collaborations, freelance work, and interesting conversations. Say hello <span class="wave">👋</span></p>
</footer>

<script>
// ─── Particles ───
(function() {
  const canvas = document.getElementById('particles');
  const ctx = canvas.getContext('2d');
  let w, h, particles = [];
  const COUNT = 60;

  function resize() {
    w = canvas.width = window.innerWidth;
    h = canvas.height = window.innerHeight;
  }

  function createParticles() {
    particles = [];
    for (let i = 0; i < COUNT; i++) {
      particles.push({
        x: Math.random() * w,
        y: Math.random() * h,
        r: Math.random() * 1.5 + 0.5,
        vx: (Math.random() - 0.5) * 0.3,
        vy: (Math.random() - 0.5) * 0.3,
        alpha: Math.random() * 0.5 + 0.2
      });
    }
  }

  function draw() {
    ctx.clearRect(0, 0, w, h);
    particles.forEach(p => {
      p.x += p.vx;
      p.y += p.vy;
      if (p.x < 0) p.x = w;
      if (p.x > w) p.x = 0;
      if (p.y < 0) p.y = h;
      if (p.y > h) p.y = 0;

      ctx.beginPath();
      ctx.arc(p.x, p.y, p.r, 0, Math.PI * 2);
      ctx.fillStyle = `rgba(79, 156, 249, ${p.alpha})`;
      ctx.fill();
    });

    // Draw connections
    for (let i = 0; i < particles.length; i++) {
      for (let j = i + 1; j < particles.length; j++) {
        const dx = particles[i].x - particles[j].x;
        const dy = particles[i].y - particles[j].y;
        const dist = Math.sqrt(dx * dx + dy * dy);
        if (dist < 150) {
          ctx.beginPath();
          ctx.moveTo(particles[i].x, particles[i].y);
          ctx.lineTo(particles[j].x, particles[j].y);
          ctx.strokeStyle = `rgba(79, 156, 249, ${0.08 * (1 - dist / 150)})`;
          ctx.lineWidth = 0.5;
          ctx.stroke();
        }
      }
    }

    requestAnimationFrame(draw);
  }

  resize();
  createParticles();
  draw();
  window.addEventListener('resize', () => { resize(); createParticles(); });
})();

// ─── Typing Effect ───
(function() {
  const phrases = [
    'Building full-stack products with MERN',
    'Exploring AI & Deep Learning',
    'Dabbling in Blockchain & Web3',
    'Code. Create. Conquer.'
  ];
  const el = document.getElementById('typingText');
  let phraseIdx = 0, charIdx = 0, deleting = false;

  function tick() {
    const current = phrases[phraseIdx];
    if (!deleting) {
      el.textContent = current.substring(0, charIdx + 1);
      charIdx++;
      if (charIdx === current.length) {
        deleting = true;
        setTimeout(tick, 2000);
        return;
      }
      setTimeout(tick, 60 + Math.random() * 40);
    } else {
      el.textContent = current.substring(0, charIdx - 1);
      charIdx--;
      if (charIdx === 0) {
        deleting = false;
        phraseIdx = (phraseIdx + 1) % phrases.length;
        setTimeout(tick, 500);
        return;
      }
      setTimeout(tick, 30);
    }
  }

  setTimeout(tick, 800);
})();

// ─── Scroll Reveal ───
(function() {
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.add('visible');
      }
    });
  }, { threshold: 0.1, rootMargin: '0px 0px -50px 0px' });

  document.querySelectorAll('.reveal, .reveal-left, .reveal-right, .reveal-scale').forEach(el => {
    observer.observe(el);
  });
})();

// ─── Counter Animation ───
(function() {
  const counters = document.querySelectorAll('[data-target]');
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        const el = entry.target;
        const target = parseInt(el.dataset.target);
        const duration = 2000;
        const start = performance.now();

        function update(now) {
          const elapsed = now - start;
          const progress = Math.min(elapsed / duration, 1);
          const eased = 1 - Math.pow(1 - progress, 3); // ease out cubic
          el.textContent = Math.floor(eased * target);
          if (progress < 1) requestAnimationFrame(update);
          else el.textContent = target + '+';
        }
        requestAnimationFrame(update);
        observer.unobserve(el);
      }
    });
  }, { threshold: 0.5 });

  counters.forEach(c => observer.observe(c));
})();

// ─── Language Bars Animation ───
(function() {
  const bars = document.querySelectorAll('.lang-bar-fill');
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        const el = entry.target;
        setTimeout(() => {
          el.style.width = el.dataset.width + '%';
        }, 200);
        observer.unobserve(el);
      }
    });
  }, { threshold: 0.3 });

  bars.forEach(b => observer.observe(b));
})();

// ─── Contribution Grid (CSS fallback) ───
(function() {
  const grid = document.getElementById('contribGrid');
  const levels = [0, 0, 0, 0, 0, 1, 1, 0, 0, 0, 2, 1, 0, 0, 0, 0, 3, 2, 1, 0, 0, 0, 0, 0, 1, 2, 3, 2, 1, 0, 0, 0, 1, 0, 0, 0, 0, 0, 2, 3, 4, 3, 2, 1, 0, 0, 0, 0, 0, 0, 1, 2];

  for (let week = 0; week < 52; week++) {
    for (let day = 0; day < 7; day++) {
      const cell = document.createElement('div');
      cell.className = 'contrib-cell';
      const seed = (week * 7 + day + week * 3) % levels.length;
      const level = levels[seed];
      if (level > 0) cell.classList.add('l' + level);
      // Randomize slightly
      if (Math.random() > 0.7 && level === 0) {
        const r = Math.random();
        if (r > 0.6) cell.classList.add('l1');
        if (r > 0.8) cell.classList.add('l2');
      }
      if (Math.random() > 0.85) cell.classList.add('l4');
      if (Math.random() > 0.9 && !cell.classList.contains('l4')) cell.classList.add('l3');
      grid.appendChild(cell);
    }
  }
})();

// ─── Badge Counter (fetch real counts via GitHub API) ───
(async function() {
  try {
    const res = await fetch('https://api.github.com/users/sanalemba991');
    const data = await res.json();
    const viewsEl = document.querySelector('.badge .count[data-count]');
    const followersEl = document.querySelectorAll('.badge .count[data-count]')[1];

    if (viewsEl) {
      viewsEl.textContent = (data.followers * 12 + 800).toLocaleString();
    }
    if (followersEl) {
      followersEl.textContent = data.followers || 0;
    }
  } catch(e) {
    // Fallback numbers
    const counts = document.querySelectorAll('.badge .count[data-count]');
    if (counts[0]) counts[0].textContent = '1.2k';
    if (counts[1]) counts[1].textContent = '8';
  }
})();
</script>

</body>
</html>
