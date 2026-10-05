/* Design Fudge Studio — Selected Works
   Progressive enhancement only: the page is fully readable without this file. */
(function () {
  "use strict";

  var reduced = window.matchMedia("(prefers-reduced-motion: reduce)").matches;

  /* ---- Scroll reveal ---------------------------------------------------- */
  var items = document.querySelectorAll(".rv");

  if (reduced || !("IntersectionObserver" in window)) {
    items.forEach(function (el) { el.classList.add("in"); });
  } else {
    var io = new IntersectionObserver(function (entries) {
      entries.forEach(function (e) {
        if (e.isIntersecting) {
          e.target.classList.add("in");
          io.unobserve(e.target);
        }
      });
    }, { rootMargin: "0px 0px -8% 0px", threshold: 0.06 });

    items.forEach(function (el) { io.observe(el); });
  }

  /* ---- Nav becomes solid once past the hero ----------------------------- */
  var nav = document.querySelector(".nav");
  var hero = document.querySelector(".hero");

  if (nav && hero && "IntersectionObserver" in window) {
    var navIO = new IntersectionObserver(function (entries) {
      nav.classList.toggle("solid", !entries[0].isIntersecting);
    }, { rootMargin: "-72px 0px 0px 0px", threshold: 0 });
    navIO.observe(hero);
  } else if (nav) {
    nav.classList.add("solid");
  }

  /* ---- Films play only while on screen, and pause when they leave -------- */
  var films = document.querySelectorAll("video[data-autoplay]");

  if (films.length) {
    if (reduced) {
      films.forEach(function (v) {
        v.removeAttribute("loop");
        v.setAttribute("controls", "");
      });
    } else if ("IntersectionObserver" in window) {
      var vio = new IntersectionObserver(function (entries) {
        entries.forEach(function (e) {
          var v = e.target;
          if (e.isIntersecting) {
            var play = v.play();
            if (play && play.catch) {
              play.catch(function () { v.setAttribute("controls", ""); });
            }
          } else if (!v.paused) {
            v.pause();
          }
        });
      }, { threshold: 0.25 });

      films.forEach(function (v) {
        v.muted = true;          // required for autoplay on iOS/Safari
        v.playsInline = true;
        vio.observe(v);
      });
    } else {
      films.forEach(function (v) { v.setAttribute("controls", ""); });
    }
  }

  /* ---- Current year in the footer -------------------------------------- */
  var yr = document.querySelector("[data-year]");
  if (yr) { yr.textContent = new Date().getFullYear(); }
})();
