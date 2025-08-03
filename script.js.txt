// JAVASCRIPT LOGIC

document.addEventListener('DOMContentLoaded', () => {

    /*----- TYPING EFFECT -----*/
    if (typeof Typed !== 'undefined') {
        new Typed('.typing-effect', {
            strings: ["AI Models.", "Intelligent Systems.", "the Future."],
            typeSpeed: 75,
            backSpeed: 50,
            loop: true
        });
    } else {
        console.error("Typed.js library not loaded.");
    }

    /*----- MOBILE NAV TOGGLE -----*/
    const navMenu = document.getElementById('nav-menu');
    const navToggle = document.getElementById('nav-toggle');
    
    if (navToggle) {
        navToggle.addEventListener('click', () => {
            navMenu.classList.toggle('show-menu');
            // Change icon
            navToggle.querySelector('i').classList.toggle('fa-bars');
            navToggle.querySelector('i').classList.toggle('fa-times');
        });
    }

    /*----- CLOSE MENU ON LINK CLICK -----*/
    const navLinks = document.querySelectorAll('.nav__link');
    navLinks.forEach(link => {
        link.addEventListener('click', () => {
            if (navMenu.classList.contains('show-menu')) {
                navMenu.classList.remove('show-menu');
                navToggle.querySelector('i').classList.add('fa-bars');
                navToggle.querySelector('i').classList.remove('fa-times');
            }
        });
    });

    /*----- STICKY HEADER & ACTIVE LINK ON SCROLL -----*/
    const header = document.getElementById('header');
    const sections = document.querySelectorAll('section[id]');
    
    function scrollHandler() {
        // Sticky Header
        if (window.scrollY >= 50) {
            header.classList.add('scrolled');
        } else {
            header.classList.remove('scrolled');
        }

        // Active Link Highlighting
        const scrollY = window.pageYOffset;
        let currentActiveSectionId = "";

        sections.forEach(current => {
            const sectionHeight = current.offsetHeight;
            const sectionTop = current.offsetTop - 100;
            const sectionId = current.getAttribute('id');
            if (scrollY >= sectionTop && scrollY < sectionTop + sectionHeight) {
                currentActiveSectionId = sectionId;
            }
        });

        navLinks.forEach(link => {
            link.classList.remove('active-link');
            if (link.getAttribute('href') === '#' + currentActiveSectionId) {
                link.classList.add('active-link');
            }
        });
    }
    
    window.addEventListener('scroll', scrollHandler);
    
    /*----- FADE-IN ANIMATION ON SCROLL -----*/
    const faders = document.querySelectorAll('.fade-in');
    const appearOptions = {
        threshold: 0.2, // Trigger when 20% of the element is in view
        rootMargin: "0px 0px -50px 0px" // Start animating a bit before it's fully in view
    };

    const appearOnScroll = new IntersectionObserver(function(entries, observer) {
        entries.forEach(entry => {
            if (!entry.isIntersecting) {
                return;
            }
            entry.target.classList.add('is-visible');
            observer.unobserve(entry.target);
        });
    }, appearOptions);

    faders.forEach(fader => {
        appearOnScroll.observe(fader);
    });

});
