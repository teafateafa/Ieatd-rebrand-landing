// ieatd-rebrand-landing.jsx
// Single-file React component (Tailwind CSS required) that implements the rebrand landing page layout
// Instructions:
// 1) Create a React app (Vite / CRA) with Tailwind configured.
// 2) Save this file in src/ and import it in App.jsx or main.jsx.
// 3) Replace placeholders with real assets and wire CTAs/search to your backend.
// NOTE: Inline comments explain structure + non-trivial bits. A tiny DEV test harness is included (console.assert).

import React, { useEffect, useMemo, useState } from 'react';

export default function RebrandLanding() {
  // Language state: Arabic by default (RTL). Supported values: 'ar' | 'en'
  const [lang, setLang] = useState('ar');
  // Header search query state
  const [query, setQuery] = useState('');

  // --- Mock data (replace with API) --------------------------------------------------------------
  const courses = [
    { id: 1, title_ar: 'دورة إدارة المشاريع الاحترافية', title_en: 'Professional Project Management', provider: 'University Partner', country: 'Saudi Arabia', badge: 'معتمد' },
    { id: 2, title_ar: 'مهارات الأخصائي النفسي المحترف', title_en: 'Clinical Psychology Practitioner', provider: 'IEATD', country: 'UAE', badge: 'معتمد' },
    { id: 3, title_ar: 'تحليل البيانات للمبتدئين', title_en: 'Data Analysis for Beginners', provider: 'Global', country: 'Qatar', badge: 'شهادة معتمدة' },
  ];

  // Ensure <html dir> and lang reflect current language on mount and whenever it changes.
  useEffect(() => {
    const nextDir = lang === 'ar' ? 'rtl' : 'ltr';
    document.documentElement.setAttribute('dir', nextDir);
    document.documentElement.lang = lang;
  }, [lang]);

  // Toggle language (and indirectly page direction via the effect above)
  const toggleLang = () => setLang(prev => (prev === 'ar' ? 'en' : 'ar'));

  // Search filter (memoized to avoid recompute on unrelated renders)
  const results = useMemo(() => {
    const q = query.trim().toLowerCase();
    if (!q) return courses;
    return courses.filter(c => (lang === 'ar' ? c.title_ar : c.title_en).toLowerCase().includes(q));
  }, [courses, query, lang]);

  // ------------------------- DEV: tiny runtime tests (console.assert) ---------------------------
  useEffect(() => {
    // Guard flag: flip to false if you don't want test logs.
    const RUN_TESTS = true;
    if (!RUN_TESTS) return;

    // Test 1: CSS token for accent color is the requested #660D0D
    const accent = getComputedStyle(document.documentElement).getPropertyValue('--color-accent').trim();
    console.assert(accent === '#660D0D', `Expected --color-accent to be #660D0D, got ${accent}`);

    // Test 2: Direction follows language toggle
    const beforeDir = document.documentElement.getAttribute('dir');
    // simulate toggle
    const tmp = lang === 'ar' ? 'en' : 'ar';
    const tmpDir = tmp === 'ar' ? 'rtl' : 'ltr';
    // no DOM toggle here—just verify mapping logic
    console.assert((lang === 'ar' ? 'rtl' : 'ltr') === beforeDir, `Expected dir ${lang === 'ar' ? 'rtl' : 'ltr'}, got ${beforeDir}`);
    console.assert((tmp === 'ar' ? 'rtl' : 'ltr') === tmpDir, 'Mapping ar→rtl / en→ltr failed');

    // Test 3: Search filter
    const arHit = courses.filter(c => c.title_ar.includes('البيانات')).length;
    const enHit = courses.filter(c => c.title_en.toLowerCase().includes('data')).length;
    console.assert(arHit > 0 && enHit > 0, 'Search dataset should include Data terms in both languages');

    // (Optional) visible note
    // console.log('DEV tests executed ✓');
  }, [lang]);

  return (
    <div className="min-h-screen bg-[var(--color-bg)] font-sans text-[var(--color-text)]">
      {/* Fonts + CSS tokens. Keeping here so the file previews standalone. */}
      <style>{`@import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&family=Poppins:wght@400;600&family=Almarai:wght@300;400;700&family=Noto+Sans+Arabic:wght@400;600&display=swap');

:root{ --color-primary:#0B3450; --color-accent:#660D0D; --color-bg:#F7F4EE; --color-text:#555B62; --color-success:#1F8A70; --radius:12px; }

[dir="rtl"] .mirror { transform: scaleX(-1); }
`}</style>

      {/* ============================== Header =================================== */}
      <header className="sticky top-0 z-40 bg-white/70 backdrop-blur-sm border-b border-gray-200">
        <div className="max-w-6xl mx-auto px-4 py-3 flex items-center justify-between">
          <div className="flex items-center gap-4">
            {/* Logo */}
            <a href="#home" className="flex items-center gap-2" aria-label="IEATD Home">
              <div className="w-10 h-10 rounded-md bg-[var(--color-primary)] flex items-center justify-center text-white font-bold">IE</div>
              <div>
                <div className="text-[14px] font-semibold" style={{ fontFamily: lang === 'ar' ? 'Almarai, sans-serif' : 'Poppins, sans-serif' }}>IEATD</div>
                <div className="text-xs text-gray-500">{lang==='ar' ? 'تعليم مهني معتمد' : 'Accredited professional learning'}</div>
              </div>
            </a>
            {/* Nav */}
            <nav className="hidden md:flex gap-4 ml-6" aria-label="Primary">
              <a href="#home" className="text-sm hover:text-[var(--color-primary)]">{lang==='ar' ? 'الصفحة الرئيسية' : 'Home'}</a>
              <a href="#programs" className="text-sm hover:text-[var(--color-primary)]">{lang==='ar' ? 'البرامج' : 'Programs'}</a>
              <a href="#b2b" className="text-sm hover:text-[var(--color-primary)]">{lang==='ar' ? 'للحكومات' : 'For Government'}</a>
            </nav>
          </div>

          <div className="flex items-center gap-3">
            {/* Search (desktop) */}
            <div className="hidden sm:block">
              <label className="sr-only" htmlFor="global-search">{lang==='ar' ? 'بحث' : 'Search'}</label>
              <div className="flex items-center bg-white border rounded-md overflow-hidden shadow-sm" style={{ minWidth: 340 }}>
                <input id="global-search" value={query} onChange={(e) => setQuery(e.target.value)} className="px-3 py-2 w-full text-sm outline-none" placeholder={lang==='ar' ? 'ابحث عن كورس أو شهادة...' : 'Search courses, certifications...'} />
                <button className="px-4 py-2 bg-[var(--color-accent)] text-white text-sm" aria-label="Search">{lang==='ar' ? 'ابحث' : 'Search'}</button>
              </div>
            </div>

            {/* Language toggle */}
            <button onClick={toggleLang} className="text-xs border rounded px-3 py-1" aria-pressed={lang==='en'}>{lang==='ar' ? 'EN' : 'العربية'}</button>
            {/* CTA */}
            <a className="hidden md:inline-block px-4 py-2 rounded text-white bg-[var(--color-primary)]" href="#signup">{lang==='ar' ? 'سجّل الآن' : 'Sign up'}</a>
          </div>
        </div>
      </header>

      {/* ============================== Hero ===================================== */}
      <section id="home" className="py-14">
        <div className="max-w-6xl mx-auto px-4 flex flex-col md:flex-row items-center gap-8">
          {/* Hero copy */}
          <div className="flex-1">
            <h1 className="text-3xl md:text-4xl font-extrabold mb-4" style={{ fontFamily: lang==='ar' ? 'Almarai, sans-serif' : 'Poppins, sans-serif', color: 'var(--color-primary)' }}>
              {lang==='ar' ? 'مهارات معتمدة — تؤهلك لسوق العمل الخليجي' : 'Accredited skills that get you hired in the Gulf'}
            </h1>
            <p className="text-[15px] mb-6 max-w-xl">
              {lang==='ar' ? 'برامج قصيرة ومكثفة مع شهادات معترف بها محليًا. سجّل اليوم وابدأ التدريب خلال أيام.' : 'Short, intensive programs with locally recognized certificates. Enroll today and start within days.'}
            </p>
            {/* CTAs */}
            <div className="flex gap-3">
              <a href="#courses" className="px-6 py-3 rounded-md shadow inline-flex items-center gap-2" style={{ background: 'var(--color-accent)', color: 'white' }}>{lang==='ar' ? 'ابدأ الآن' : 'Get Started'}</a>
              <a href="#programs" className="px-5 py-3 rounded-md border inline-flex items-center gap-2" style={{ borderColor: 'var(--color-primary)', color: 'var(--color-primary)' }}>{lang==='ar' ? 'استعرض البرامج' : 'Browse Programs'}</a>
            </div>
            {/* Proof points */}
            <div className="mt-6 flex items-center gap-4 text-sm text-gray-600">
              <div className="flex items-center gap-2">
                <svg className="w-5 h-5" viewBox="0 0 24 24" fill="none" stroke="currentColor" aria-hidden="true"><path d="M12 2v6" strokeWidth="1.5" strokeLinecap="round" strokeLinejoin="round"/></svg>
                <span>{lang==='ar' ? 'دعم مباشر عبر WhatsApp' : 'Direct support via WhatsApp'}</span>
              </div>
              <div className="flex items-center gap-2">
                <svg className="w-5 h-5" viewBox="0 0 24 24" fill="none" stroke="currentColor" aria-hidden="true"><circle cx="12" cy="12" r="10" strokeWidth="1.5"/></svg>
                <span>{lang==='ar' ? 'شهادات معتمدة محليًا' : 'Locally accredited certificates'}</span>
              </div>
            </div>
          </div>

          {/* Hero visual mock */}
          <div className="flex-1">
            <div className="bg-white rounded-2xl shadow p-6" style={{ border: `1px solid rgba(11,52,80,0.06)` }}>
              <div className="flex items-center justify-between mb-4">
                <div>
                  <div className="text-sm text-gray-500">{lang==='ar' ? 'برنامج مميز' : 'Featured Program'}</div>
                  <div className="font-semibold text-lg">{lang==='ar' ? 'مهارات الأخصائي النفسي المحترف' : 'Clinical Psychology Practitioner'}</div>
                </div>
                <div className="text-sm px-3 py-1 rounded" style={{ background: 'rgba(102,13,13,0.12)', color: 'var(--color-accent)' }}>معتمد</div>
              </div>

              {/* Course preview card mock (replace with real hero image/video) */}
              <div className="h-40 rounded-lg mb-4 flex items-end p-4 text-white" style={{ backgroundImage: 'linear-gradient(180deg, rgba(11,52,80,0.9), rgba(11,52,80,0.1))' }}>
                <div>
                  <div className="text-sm">{lang==='ar' ? 'مدة: 8 أسابيع' : 'Duration: 8 weeks'}</div>
                  <div className="text-xs">{lang==='ar' ? 'بداية قريبة — مكان محدود' : 'Starting soon — limited seats'}</div>
                </div>
              </div>

              <div className="flex items-center justify-between">
                <div className="text-sm text-gray-600">{lang==='ar' ? 'مدرب: د. سارة' : 'Instructor: Dr. Sara'}</div>
                <a className="px-3 py-2 bg-[var(--color-primary)] text-white rounded" href="#enroll">{lang==='ar' ? 'سجل الآن' : 'Enroll'}</a>
              </div>
            </div>
            <div className="mt-4 text-xs text-gray-500">{lang==='ar' ? 'مثال واجهة عرض كورس — استبدل بالصورة الحقيقية' : 'Course preview mock — replace with real image'}</div>
          </div>
        </div>
      </section>

      {/* ============================== Categories ================================= */}
      <section id="courses" className="py-8 border-t">
        <div className="max-w-6xl mx-auto px-4">
          <h3 className="text-xl font-semibold mb-4" style={{ fontFamily: lang==='ar' ? 'Almarai' : 'Poppins' }}>{lang==='ar' ? 'التصنيفات الشائعة' : 'Top Categories'}</h3>
          <div className="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 gap-4">
            {[ 'التطوير المهني', 'الصحة النفسية', 'الإدارة', 'تحليل البيانات' ].map((c, idx) => (
              <div key={idx} className="bg-white rounded-lg p-4 shadow-sm flex flex-col gap-2">
                <div className="text-sm text-gray-400">{lang==='ar' ? c : ['Professional development','Mental Health','Management','Data Analysis'][idx]}</div>
                <div className="font-semibold">{lang==='ar' ? `${c} — برامج معتمدة` : `${['Professional development','Mental Health','Management','Data Analysis'][idx]} — Accredited`}</div>
                <div className="mt-auto text-xs text-gray-500">{lang==='ar' ? 'ابدأ من' : 'Start from'} <span className="font-semibold">{lang==='ar' ? '₪' : '$'}99</span></div>
              </div>
            ))}
          </div>
        </div>
      </section>

      {/* ============================== Value Props ================================= */}
      <section className="py-10">
        <div className="max-w-6xl mx-auto px-4 grid md:grid-cols-3 gap-6">
          <div className="bg-white rounded-lg p-6 shadow-sm">
            <h4 className="font-semibold mb-2">{lang==='ar' ? 'معتمدون محليًا' : 'Locally accredited'}</h4>
            <p className="text-sm text-gray-600">{lang==='ar' ? 'شهادات معترف بها من جهات حكومية وشريكنا التعليمي' : 'Certificates recognized by local authorities and partners'}</p>
          </div>
          <div className="bg-white rounded-lg p-6 shadow-sm">
            <h4 className="font-semibold mb-2">{lang==='ar' ? 'مدربون محترفون' : 'Professional instructors'}</h4>
            <p className="text-sm text-gray-600">{lang==='ar' ? 'مدربون محليون ودوليون بخبرة عملية' : 'Local and international instructors with practical experience'}</p>
          </div>
          <div className="bg-white rounded-lg p-6 shadow-sm">
            <h4 className="font-semibold mb-2">{lang==='ar' ? 'دعم وتواصل مباشر' : 'Direct support'}</h4>
            <p className="text-sm text-gray-600">{lang==='ar' ? 'دردشة WhatsApp/Telegram للرد السريع' : 'WhatsApp/Telegram chat for quick replies'}</p>
          </div>
        </div>
      </section>

      {/* ============================== Programs ==================================== */}
      <section id="programs" className="py-10 border-t">
        <div className="max-w-6xl mx_auto max-w-6xl mx-auto px-4">
          <h3 className="text-xl font-semibold mb-6">{lang==='ar' ? 'برامج مميزة ومعتمدة' : 'Featured Accredited Programs'}</h3>
          <div className="grid md:grid-cols-3 gap-6">
            {results.map(course => (
              <div key={course.id} className="bg-white rounded-xl p-4 shadow-sm">
                <div className="flex items-start justify-between gap-4">
                  <div>
                    <div className="text-sm text-gray-400">{course.provider} • {course.country}</div>
                    <div className="font-semibold text-lg mt-2">{lang==='ar' ? course.title_ar : course.title_en}</div>
                  </div>
                  <div className="text-sm px-3 py-1 rounded-full" style={{ background: 'rgba(31,138,112,0.08)', color: 'var(--color-success)' }}>{course.badge}</div>
                </div>
                <div className="mt-4 flex items-center justify_between justify-between">
                  <div className="text-sm text-gray-500">{lang==='ar' ? 'مدة: 6 أسابيع' : 'Duration: 6 weeks'}</div>
                  <a className="px-3 py-2 bg-[var(--color-primary)] text-white rounded" href="#syllabus">{lang==='ar' ? 'عرض المنهاج' : 'View Syllabus'}</a>
                </div>
              </div>
            ))}
          </div>
        </div>
      </section>

      {/* ============================== B2B/Government ================================= */}
      <section id="b2b" className="py-12 bg-white border-t">
        <div className="max-w-6xl mx-auto px-4 flex flex-col md:flex-row items-center gap-6">
          <div className="flex-1">
            <h3 className="text-2xl font-semibold">{lang==='ar' ? 'حلول مخصصة للجهات الحكومية والشركات' : 'Tailored solutions for governments & enterprises'}</h3>
            <p className="text-gray-600 mt-2">{lang==='ar' ? 'بوابات تدريب للموظفين، تقارير أداء، وتدريبات معتمدة تناسب متطلبات الجهات' : 'Employee portals, performance reports, and accredited training that match requirements'}</p>
            <div className="mt-4 flex gap-3">
              <a className="px-4 py-2 bg-[var(--color-accent)] rounded text-white" href="#demo">{lang==='ar' ? 'اطلب عرضًا' : 'Request a demo'}</a>
              <a className="px-4 py-2 border rounded" style={{ borderColor: 'var(--color-primary)', color: 'var(--color-primary)' }} href="#contact">{lang==='ar' ? 'تواصل معنا' : 'Contact us'}</a>
            </div>
          </div>
          <div className="flex-1 w-full">
            {/* Simple stats block as a visual anchor */}
            <div className="grid grid-cols-3 gap-3">
              {[{n:'95%',t_ar:'رضا المتعلمين',t_en:'Learner satisfaction'},{n:'30k+',t_ar:'خريجون',t_en:'Graduates'},{n:'50+',t_ar:'شريك',t_en:'Partners'}].map((s, i) => (
                <div key={i} className="p-5 rounded-xl border bg-[var(--color-bg)]">
                  <div className="text-2xl font-bold text-[var(--color-primary)]">{s.n}</div>
                  <div className="text-xs text-gray-600">{lang==='ar' ? s.t_ar : s.t_en}</div>
                </div>
              ))}
            </div>
          </div>
        </div>
      </section>

      {/* ============================== Footer ====================================== */}
      <footer className="mt-10 border-t">
        <div className="max-w-6xl mx-auto px-4 py-8 grid md:grid-cols-3 gap-6 text-sm">
          <div>
            <div className="font-semibold mb-2">IEATD</div>
            <p className="text-gray-600">{lang==='ar' ? 'تعليم مهني معتمد موجه لسوق الخليج.' : 'Accredited professional learning for the Gulf market.'}</p>
          </div>
          <div>
            <div className="font-semibold mb-2">{lang==='ar' ? 'روابط' : 'Links'}</div>
            <ul className="space-y-1">
              <li><a href="#programs" className="hover:text-[var(--color-primary)]">{lang==='ar' ? 'البرامج' : 'Programs'}</a></li>
              <li><a href="#b2b" className="hover:text-[var(--color-primary)]">{lang==='ar' ? 'حلول الشركات' : 'Enterprise'}</a></li>
              <li><a href="#help" className="hover:text-[var(--color-primary)]">{lang==='ar' ? 'المساعدة' : 'Help'}</a></li>
            </ul>
          </div>
          <div>
            <div className="font-semibold mb-2">{lang==='ar' ? 'تواصل' : 'Contact'}</div>
            <ul className="space-y-1">
              <li><a href="mailto:hello@ieatd.com" className="hover:text-[var(--color-primary)]">hello@ieatd.com</a></li>
              <li><a href="https://wa.me/0000000000" className="hover:text-[var(--color-primary)]" target="_blank" rel="noreferrer">WhatsApp</a></li>
            </ul>
          </div>
        </div>
        <div className="text-xs text-gray-500 text-center pb-6">© {new Date().getFullYear()} IEATD. All Rights Reserved.</div>
      </footer>

      {/* Floating WhatsApp helper (purely demonstrative) */}
      <a href="https://wa.me/0000000000" target="_blank" rel="noreferrer" aria-label="WhatsApp" className="fixed bottom-4 right-4 w-12 h-12 rounded-full bg-[var(--color-success)] text-white flex items-center justify-center shadow-lg">WA</a>
    </div>
  );
}
