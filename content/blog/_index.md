+++
title = "Blog"
description = "Long-form posts (coming soon)."
sort_by = "date"
paginate_by = 5
+++
<style>
.blog-empty {
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
    gap: 0.5rem;
    padding: 2.5rem 1rem;
}

.blog-empty-art {
    width: 220px;
    height: auto;
    margin-bottom: 0.5rem;
    filter: var(--icon-filter, none);
}

.blog-empty p {
    margin: 0;
    color: var(--text-1);
}

.blog-empty-sub {
    font-size: 0.9rem;
    color: var(--text-2, #888);
}
</style>

<div class="blog-empty"><img class="blog-empty-art" src="/img/blog-draft.svg" alt="" width="220" height="130" /><p>Nothing here yet, first post is brewing.</p><p class="blog-empty-sub">Check back soon, or browse the <a href="/notes/">tech notes</a> in the meantime.</p></div>
