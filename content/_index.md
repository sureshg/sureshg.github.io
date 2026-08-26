+++
title = "Suresh"
template = "homepage.html"
+++

<style>
.profile-card {
    position: relative;
    overflow: hidden;
    text-align: center;
    padding: 2rem 1.5rem;
    margin: 1rem 0 2.5rem;
    border: 1px solid var(--border-color, #ddd);
    border-radius: 22px;
    background:
        radial-gradient(circle at 15% 20%, rgba(99, 102, 241, 0.14), transparent 38%),
        radial-gradient(circle at 85% 80%, rgba(14, 165, 233, 0.12), transparent 38%),
        var(--bg-1, #f5f5f5);
}

.profile-photo {
    width: 132px;
    height: 132px;
    border-radius: 50%;
    overflow: hidden;
    margin: 0 auto 1.25rem;
    border: 4px solid var(--bg-0, #fff);
    box-shadow: 0 10px 30px rgba(15, 23, 42, 0.18);
}

.profile-photo img {
    width: 100%;
    height: 100%;
    object-fit: cover;
}

.profile-bio {
    color: var(--text-1);
    max-width: 620px;
    margin: 0 auto;
    line-height: 1.6;
}

.home-section {
    margin: 0 0 2.25rem;
}

.home-section-header {
    display: flex;
    align-items: baseline;
    justify-content: space-between;
    gap: 1rem;
    margin-bottom: 0.9rem;
}

.home-section-title {
    margin: 0;
    font-size: 1.15rem;
    font-weight: 700;
    letter-spacing: -0.02em;
}

.home-section-label {
    color: var(--text-1, #666);
    font-size: 0.78rem;
}

.home-cards {
    display: grid;
    grid-template-columns: repeat(3, minmax(0, 1fr));
    gap: 0.75rem;
}

.home-card {
    --card-accent: #6366f1;
    --card-glow: rgba(99, 102, 241, 0.12);
    position: relative;
    overflow: hidden;
    display: flex;
    flex-direction: column;
    gap: 0.45rem;
    min-height: 118px;
    padding: 1rem;
    color: inherit;
    border-radius: 16px;
    background:
        radial-gradient(circle at 100% 0, var(--card-glow), transparent 45%),
        var(--bg-1, #f5f5f5);
    border: 1px solid var(--border-color, #ddd);
    text-decoration: none;
    transition: transform 0.2s ease, border-color 0.2s ease, box-shadow 0.2s ease;
}

.home-card:hover {
    color: inherit;
    border-color: var(--border-color, #ddd);
    background:
        radial-gradient(circle at 100% 0, var(--card-glow), transparent 60%),
        radial-gradient(circle at 0 100%, rgba(99, 102, 241, 0.06), transparent 55%),
        var(--bg-1, #f5f5f5);
    transform: translateY(-2px);
    box-shadow: 0 10px 26px rgba(15, 23, 42, 0.09);
}

.home-card:focus-visible {
    outline: 3px solid var(--card-accent);
    outline-offset: 3px;
}

.home-card-icon {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 34px;
    height: 34px;
    color: var(--card-accent);
    border-radius: 11px;
    background: var(--card-glow);
    flex-shrink: 0;
}

.home-card-icon svg {
    width: 18px;
    height: 18px;
    fill: none;
    stroke: currentColor;
    stroke-width: 2;
    stroke-linecap: round;
    stroke-linejoin: round;
}

.home-card-title {
    margin: 0;
    font-size: 0.95rem;
    font-weight: 700;
    letter-spacing: -0.015em;
}

.home-card-desc {
    margin: 0;
    font-size: 0.8rem;
    color: var(--text-1, #666);
    line-height: 1.5;
}

.home-card-meta {
    margin-top: auto;
    color: var(--text-1, #666);
    font-size: 0.68rem;
    font-weight: 400;
}

@media (max-width: 640px) {
    .profile-card {
        padding: 1.5rem 1rem;
        border-radius: 18px;
    }

    .home-cards {
        grid-template-columns: 1fr;
    }

    .home-section-label {
        display: none;
    }
}

@media (min-width: 641px) and (max-width: 820px) {
    .home-cards {
        grid-template-columns: repeat(2, minmax(0, 1fr));
    }
}

@media (prefers-reduced-motion: reduce) {
    .home-card {
        transition: none;
    }
}
</style>

<div class="profile-card"><div class="profile-photo"><img src="/img/profile.jpg" alt="Suresh" /></div><p class="profile-bio">Backend Developer | OSS | Java | Kotlin Multiplatform (JVM, Native, Wasm, JS) | OpenJDK | GraalVM | Agentic AI</p></div>

<section class="home-section"><div class="home-section-header"><h2 class="home-section-title">Apps</h2><span class="home-section-label">Small, useful tools</span></div><div class="home-cards">
<a class="home-card" style="--card-accent: #f59e0b; --card-glow: rgba(245, 158, 11, 0.14);" href="/app/hn/"><span class="home-card-icon" aria-hidden="true"><svg viewBox="0 0 24 24"><circle cx="11" cy="11" r="8"/><path d="m21 21-4.3-4.3"/></svg></span><h3 class="home-card-title">HN Search</h3><p class="home-card-desc">Multi-term search for Hacker News posts and comments.</p><span class="home-card-meta">Web app</span></a>
<a class="home-card" style="--card-accent: #8b5cf6; --card-glow: rgba(139, 92, 246, 0.14);" href="/app/trace-viewer/"><span class="home-card-icon" aria-hidden="true"><svg viewBox="0 0 24 24"><path d="M3 3v18h18"/><path d="m7 16 4-5 4 3 5-7"/></svg></span><h3 class="home-card-title">Trace Viewer</h3><p class="home-card-desc">Visualize Kotlin Toolchain build traces right in the browser.</p><span class="home-card-meta">Developer tool</span></a>
</div></section>

<section class="home-section"><div class="home-section-header"><h2 class="home-section-title">Libraries &amp; Tools</h2><span class="home-section-label">Open source on GitHub</span></div><div class="home-cards">
<a class="home-card" style="--card-accent: #0ea5e9; --card-glow: rgba(14, 165, 233, 0.14);" href="https://github.com/sureshg/kotlin-vipaccess" target="_blank" rel="noopener"><span class="home-card-icon" aria-hidden="true"><svg viewBox="0 0 24 24"><path d="M20 13c0 5-3.5 7.5-8 9-4.5-1.5-8-4-8-9V5l8-3 8 3z"/><circle cx="12" cy="11" r="2"/><path d="M12 13v3"/></svg></span><h3 class="home-card-title">Kotlin VIP Access</h3><p class="home-card-desc">Kotlin Multiplatform support for Symantec VIP Access TOTP tokens.</p><span class="home-card-meta">Kotlin Multiplatform</span></a>
<a class="home-card" style="--card-accent: #10b981; --card-glow: rgba(16, 185, 129, 0.14);" href="https://github.com/sureshg/certkit" target="_blank" rel="noopener"><span class="home-card-icon" aria-hidden="true"><svg viewBox="0 0 24 24"><path d="M15 7a2 2 0 1 0-4 0 2 2 0 0 0 4 0Z"/><path d="M13 2v3M13 9v3M8.5 4.5l2 2M15.5 9.5l2 2M8 7h3M15 7h3M8.5 9.5l2-2M15.5 4.5l2-2"/><path d="M6 13h14v9H6z"/><path d="M10 17h6"/></svg></span><h3 class="home-card-title">CertKit</h3><p class="home-card-desc">Lightweight X.509, PEM/DER, CSR and CRL toolkit for Kotlin/JVM.</p><span class="home-card-meta">Kotlin · Security</span></a>
<a class="home-card" style="--card-accent: #6366f1; --card-glow: rgba(99, 102, 241, 0.14);" href="https://github.com/sureshg/protobuf-toolchain-plugin" target="_blank" rel="noopener"><span class="home-card-icon" aria-hidden="true"><svg viewBox="0 0 24 24"><path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"/><path d="M14 2v6h6M10 13l-2 2 2 2M14 13l2 2-2 2"/></svg></span><h3 class="home-card-title">Protobuf Toolchain Plugin</h3><p class="home-card-desc">Generate Java, Kotlin and gRPC code from proto files without native protoc.</p><span class="home-card-meta">Build plugin</span></a>
<a class="home-card" style="--card-accent: #ec4899; --card-glow: rgba(236, 72, 153, 0.14);" href="https://github.com/sureshg/kmp-play" target="_blank" rel="noopener"><span class="home-card-icon" aria-hidden="true"><svg viewBox="0 0 24 24"><path d="M9 3h6M10 9V3h4v6l5 9a2 2 0 0 1-2 3H7a2 2 0 0 1-2-3z"/><path d="M7.5 15h9"/></svg></span><h3 class="home-card-title">KMP Playground</h3><p class="home-card-desc">Kotlin Multiplatform and JVM playground powered by Kotlin Toolchain.</p><span class="home-card-meta">Kotlin Multiplatform</span></a>
<a class="home-card" style="--card-accent: #f97316; --card-glow: rgba(249, 115, 22, 0.14);" href="https://github.com/sureshg/kdeb" target="_blank" rel="noopener"><span class="home-card-icon" aria-hidden="true"><svg viewBox="0 0 24 24"><path d="m7.5 4.3 9 5.2M3.3 7l8.7 5 8.7-5M12 22V12"/><path d="m21 16-9 6-9-6V8l9-6 9 6z"/></svg></span><h3 class="home-card-title">kdeb</h3><p class="home-card-desc">Build Debian packages in pure Kotlin with a type-safe DSL.</p><span class="home-card-meta">Kotlin Multiplatform</span></a>
<a class="home-card" style="--card-accent: #14b8a6; --card-glow: rgba(20, 184, 166, 0.14);" href="https://github.com/sureshg/truststore-scan" target="_blank" rel="noopener"><span class="home-card-icon" aria-hidden="true"><svg viewBox="0 0 24 24"><path d="M20 13c0 5-3.5 7.5-8 9-4.5-1.5-8-4-8-9V5l8-3 8 3z"/><path d="m9 12 2 2 4-4"/></svg></span><h3 class="home-card-title">TrustStore Scan</h3><p class="home-card-desc">Scan JDK, system and custom trust stores for certificates.</p><span class="home-card-meta">Java · Security</span></a>
</div></section>
