/* Shared behaviour: theme, EN/TR toggle, progress bar, lightbox.
   Per page: define `const i18n = {en:{...}, tr:{...}}` BEFORE loading this file. */
(function () {
  var d = document.documentElement;
  function get(k) { try { return localStorage.getItem(k); } catch (e) { return null; } }
  function set(k, v) { try { localStorage.setItem(k, v); } catch (e) {} }

  d.setAttribute('data-theme', get('theme') || 'light');

  window.applyLang = function (lang) {
    var t = (typeof i18n !== 'undefined' && i18n[lang]) || {};
    d.setAttribute('data-lang', lang);
    d.lang = lang;
    if (t.page_title) document.title = t.page_title;
    document.querySelectorAll('[data-i18n]').forEach(function (el) {
      var v = t[el.getAttribute('data-i18n')];
      if (v !== undefined) el.innerHTML = v;
    });
    var b = document.getElementById('lang-toggle');
    if (b) b.textContent = lang === 'en' ? 'TR' : 'EN';
    set('lang', lang);
  };

  window.openLightbox = function (src) {
    var lb = document.getElementById('lightbox');
    if (!lb) return;
    document.getElementById('lightbox-img').src = src;
    lb.classList.add('open');
  };

  document.addEventListener('DOMContentLoaded', function () {
    var tt = document.getElementById('light-toggle');
    if (tt) tt.addEventListener('click', function () {
      var n = d.getAttribute('data-theme') === 'light' ? 'dark' : 'light';
      d.setAttribute('data-theme', n);
      set('theme', n);
    });

    window.applyLang(get('lang') || 'en');
    var lt = document.getElementById('lang-toggle');
    if (lt) lt.addEventListener('click', function () {
      window.applyLang(d.getAttribute('data-lang') === 'en' ? 'tr' : 'en');
    });

    var p = document.getElementById('progress');
    if (p) {
      p.max = 100;
      document.addEventListener('scroll', function () {
        var h = d.scrollHeight - window.innerHeight;
        p.value = h > 0 ? (window.scrollY / h) * 100 : 0;
      });
    }

    var lb = document.getElementById('lightbox');
    if (lb) {
      var close = function () { lb.classList.remove('open'); };
      lb.addEventListener('click', close);
      document.addEventListener('keydown', function (e) { if (e.key === 'Escape') close(); });
    }
  });
})();
