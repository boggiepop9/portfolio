/* =========================================================
   main.js — Tristan Panniers Portfolio
   ========================================================= */

// ── Navbar scroll effect ──────────────────────────────────
const navbar = document.getElementById('navbar');

function handleNavScroll() {
  if (window.scrollY > 60) {
    navbar.classList.add('navbar-scrolled');
  } else {
    navbar.classList.remove('navbar-scrolled');
  }
}

window.addEventListener('scroll', handleNavScroll, { passive: true });
handleNavScroll(); // run once on load

// ── Mobile menu ───────────────────────────────────────────
const menuBtn    = document.getElementById('menu-btn');
const mobileMenu = document.getElementById('mobile-menu');
const bar1       = document.getElementById('bar1');
const bar2       = document.getElementById('bar2');
const bar3       = document.getElementById('bar3');
let menuOpen = false;

function openMenu() {
  menuOpen = true;
  mobileMenu.classList.remove('hidden');
  // Animate to X
  bar1.style.transform = 'rotate(45deg) translate(5px, 6px)';
  bar2.style.opacity   = '0';
  bar3.style.transform = 'rotate(-45deg) translate(5px, -6px)';
  bar3.style.width     = '24px';
}

function closeMenu() {
  menuOpen = false;
  mobileMenu.classList.add('hidden');
  bar1.style.transform = '';
  bar2.style.opacity   = '';
  bar3.style.transform = '';
  bar3.style.width     = '';
}

menuBtn.addEventListener('click', () => menuOpen ? closeMenu() : openMenu());

document.querySelectorAll('.mobile-nav-link').forEach(link => {
  link.addEventListener('click', closeMenu);
});

// ── Scroll-reveal (Intersection Observer) ─────────────────
const revealObserver = new IntersectionObserver(
  (entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.add('is-visible');
        revealObserver.unobserve(entry.target); // fire once
      }
    });
  },
  { threshold: 0.12, rootMargin: '0px 0px -48px 0px' }
);

document.querySelectorAll('.reveal').forEach(el => revealObserver.observe(el));

// ── Active nav link highlight on scroll ──────────────────
const sections  = document.querySelectorAll('section[id]');
const navLinks  = document.querySelectorAll('.nav-link');

const sectionObserver = new IntersectionObserver(
  (entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        const id = entry.target.getAttribute('id');
        navLinks.forEach(link => {
          const active = link.getAttribute('href') === `#${id}`;
          link.classList.toggle('text-white',    active);
          link.classList.toggle('text-slate-300', !active);
        });
      }
    });
  },
  { rootMargin: '-40% 0px -55% 0px' }
);

sections.forEach(s => sectionObserver.observe(s));

// ── Demo Reel playlist ────────────────────────────────────
const reelPlayer = document.getElementById('reel-player');
const reelTitle  = document.getElementById('reel-title');
const reelDesc   = document.getElementById('reel-desc');
const reelItems  = document.querySelectorAll('.reel-item');

reelItems.forEach(item => {
  item.addEventListener('click', () => {
    reelItems.forEach(el => el.classList.remove('reel-item--active'));
    item.classList.add('reel-item--active');
    reelPlayer.src   = item.dataset.src;
    reelTitle.textContent = item.dataset.title;
    reelDesc.innerHTML    = item.dataset.desc;
  });
});

// ── Contact form (Formspree) ──────────────────────────────
const contactForm = document.getElementById('contact-form');

if (contactForm) {
  contactForm.addEventListener('submit', async (e) => {
    e.preventDefault();
    const btn = contactForm.querySelector('button[type="submit"]');
    const original = btn.textContent;

    btn.textContent = 'Sending…';
    btn.disabled    = true;

    try {
      const response = await fetch('https://formspree.io/f/mwvakrgz', {
        method:  'POST',
        headers: { 'Accept': 'application/json' },
        body:    new FormData(contactForm),
      });

      if (response.ok) {
        btn.textContent = '✓ Message Sent!';
        contactForm.reset();
        setTimeout(() => {
          btn.textContent = original;
          btn.disabled    = false;
        }, 3000);
      } else {
        btn.textContent = 'Something went wrong — please try again.';
        btn.disabled    = false;
      }
    } catch {
      btn.textContent = 'Network error — please try again.';
      btn.disabled    = false;
    }
  });
}
