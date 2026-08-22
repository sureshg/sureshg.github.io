+++
title = "Suresh"
template = "homepage.html"
+++

<style>
.profile-card {
    text-align: center;
    padding: 1.5rem 0 0.5rem;
}

.profile-photo {
    width: 140px;
    height: 140px;
    border-radius: 50%;
    overflow: hidden;
    margin: 0 auto 1.25rem;
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.15);
}

.profile-photo img {
    width: 100%;
    height: 100%;
    object-fit: cover;
}

.profile-bio {
    color: var(--text-1);
    max-width: 560px;
    margin: 0 auto;
    line-height: 1.6;
}

.home-cards {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
    gap: 1rem;
    margin-top: 0.75rem;
}

.home-card {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
    padding: 1.25rem;
    border-radius: 12px;
    background: var(--bg-1, #f5f5f5);
    border: 1px solid var(--border-color, #ddd);
    transition: transform 0.15s ease, box-shadow 0.15s ease;
}

.home-card:hover {
    transform: translateY(-3px);
    box-shadow: 0 8px 24px rgba(0, 0, 0, 0.12);
}

.home-card-icon {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 34px;
    height: 34px;
    border-radius: 50%;
    background: var(--bg-2, #eee);
    flex-shrink: 0;
}

.home-card-icon img {
    width: 17px;
    height: 17px;
    filter: var(--icon-filter, none);
}

.home-card-title {
    margin: 0;
    font-size: 1.05rem;
    font-weight: 600;
}

.home-card-title a {
    color: inherit;
}

.home-card-desc {
    margin: 0;
    font-size: 0.9rem;
    color: var(--text-1, #666);
    line-height: 1.5;
}
</style>

<div class="profile-card"><div class="profile-photo"><img src="/img/profile.jpg" alt="Suresh" /></div><p class="profile-bio">Backend Developer | OSS | Java | Kotlin Multiplatform (JVM, Native, Wasm, JS) | OpenJDK | GraalVM | Agentic AI</p></div>

<div class="home-cards"><div class="home-card"><div class="home-card-icon"><img src="/icons/notebook-text.svg" alt="" /></div><h3 class="home-card-title"><a href="/notes/">Tech Notes</a></h3><p class="home-card-desc">Cheat sheets and reference notes on the JVM, Kotlin, containers, security, certificates and Linux.</p></div><div class="home-card"><div class="home-card-icon"><img src="/icons/search.svg" alt="" /></div><h3 class="home-card-title"><a href="/app/hn/">HN Search</a></h3><p class="home-card-desc">A simple multi-term search for Hacker News posts and comments.</p></div><div class="home-card"><div class="home-card-icon"><img src="/icons/code.svg" alt="" /></div><h3 class="home-card-title"><a href="/app/trace-viewer/">Trace Viewer</a></h3><p class="home-card-desc">Visualizes Kotlin Toolchain build traces in the browser.</p></div></div>
