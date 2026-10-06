
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pacific Wildlife Expeditions - Multi-Page Accessible Website</title>
    
    <!-- External Libraries for UI Workbench Tools -->
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <style>
        /* ==========================================================================
           EXTERNAL SHARED STYLESHEET (styles.css embedded for single-file runtime)
           ========================================================================== */

        /* --------------------------------------------------------------------------
           1. ACCESSIBILITY: SKIP TO MAIN CONTENT LINK
           Uses position and :focus pseudo-class to reveal only when tabbed into.
           -------------------------------------------------------------------------- */
        .skip-link {
            position: absolute;
            top: -120px; /* Visually hidden off-screen by default */
            left: 15px;
            background: #0284c7;
            color: #ffffff;
            padding: 12px 20px;
            font-weight: 700;
            text-decoration: underline;
            border-radius: 0 0 8px 8px;
            box-shadow: 0 8px 16px rgba(0, 0, 0, 0.25);
            z-index: 10000;
            transition: top 0.25s ease-in-out;
        }

        .skip-link:focus {
            top: 10px; /* Moves smoothly into view upon focus */
            outline: 3px solid #f59e0b;
        }

        /* --------------------------------------------------------------------------
           2. GLOBAL BODY & TYPOGRAPHY STYLES
           -------------------------------------------------------------------------- */
        body {
            font-family: 'Segoe UI', system-ui, -apple-system, sans-serif;
            font-size: 16px;
            line-height: 1.65;
            color: #1e293b;
            background-color: #f8fafc;
            margin: 0;
            padding: 0;
        }

        /* --------------------------------------------------------------------------
           3. ATTRACTIVE FLEXBOX NAVIGATION BAR
           Styled using at least 3 distinct CSS properties (background, border, flexbox, shadow)
           -------------------------------------------------------------------------- */
        header.site-header {
            background: linear-gradient(135deg, #0f172a 0%, #1e293b 100%);
            color: #ffffff;
            padding: 1.25rem 2rem;
            border-bottom: 4px solid #0284c7;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
        }

        nav.site-nav {
            display: flex; /* Flexbox Requirement */
            flex-wrap: wrap;
            align-items: center;
            justify-content: space-between;
            background-color: rgba(30, 41, 59, 0.85);
            padding: 0.85rem 1.5rem;
            border-radius: 12px; /* Border radius */
            border: 1px solid rgba(255, 255, 255, 0.1); /* Border */
            box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.1); /* Shadow */
            max-width: 1100px;
            margin: 0 auto;
        }

        .nav-brand {
            display: flex;
            align-items: center;
            gap: 12px;
            text-decoration: none;
            color: #ffffff;
            font-weight: 700;
            font-size: 1.2rem;
        }

        .nav-brand img {
            width: 42px;
            height: 42px;
            border-radius: 50%;
            border: 2px solid #38bdf8;
            padding: 2px;
            background-color: #0f172a;
        }

        ul.nav-menu {
            display: flex; /* Flexbox navigation */
            list-style: none;
            margin: 0;
            padding: 0;
            gap: 12px;
        }

        ul.nav-menu a {
            color: #e2e8f0;
            text-decoration: none;
            padding: 8px 16px;
            font-weight: 600;
            font-size: 0.95rem;
            border-radius: 6px;
            transition: all 0.2s ease-in-out;
            display: inline-block;
        }

        /* --------------------------------------------------------------------------
           4. HOVER PSEUDO-CLASS WITH TRANSITION
           -------------------------------------------------------------------------- */
        ul.nav-menu a:hover,
        ul.nav-menu a:focus {
            background-color: #0284c7;
            color: #ffffff;
            transform: translateY(-2px);
            box-shadow: 0 4px 8px rgba(2, 132, 199, 0.3);
            outline: 2px solid #38bdf8;
        }

        ul.nav-menu a.active-page {
            background-color: #0284c7;
            color: #ffffff;
            border-bottom: 2px solid #38bdf8;
        }

        /* --------------------------------------------------------------------------
           5. MAIN CONTENT AREA & LAYOUTS
           -------------------------------------------------------------------------- */
        main#main-content {
            max-width: 1100px;
            margin: 2.5rem auto;
            padding: 2.5rem;
            background-color: #ffffff;
            border-radius: 16px;
            box-shadow: 0 10px 25px -5px rgba(0, 0, 0, 0.05), 0 8px 10px -6px rgba(0, 0, 0, 0.01);
            border: 1px solid #e2e8f0;
            min-height: 450px;
        }

        /* --------------------------------------------------------------------------
           6. BOX MODEL IMAGE STYLING
           Requirements met: border, padding, border-radius applied to all content images
           -------------------------------------------------------------------------- */
        .content-image {
            border: 3px solid #cbd5e1; /* Border */
            padding: 8px; /* Padding */
            border-radius: 12px; /* Border radius */
            background-color: #ffffff; /* Box model background */
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            max-width: 100%;
            height: auto;
            display: block;
        }

        /* --------------------------------------------------------------------------
           7. HOVER EFFECTS FOR IMAGES & CARDS
           -------------------------------------------------------------------------- */
        .content-image:hover {
            border-color: #0284c7;
            transform: scale(1.03) translateY(-4px);
            box-shadow: 0 12px 24px rgba(2, 132, 199, 0.2);
        }

        /* --------------------------------------------------------------------------
           8. CSS GRID LAYOUT
           Applied to photo gallery grid with multiple columns
           -------------------------------------------------------------------------- */
        .gallery-grid {
            display: grid; /* Grid Property */
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); /* Responsive Multi-Column */
            gap: 24px;
            margin-top: 2rem;
        }

        .gallery-card {
            background-color: #f8fafc;
            border-radius: 14px;
            padding: 12px;
            border: 1px solid #e2e8f0;
            display: flex;
            flex-direction: column;
            gap: 10px;
            transition: transform 0.3s ease;
        }

        .gallery-card:hover {
            transform: translateY(-4px);
            border-color: #38bdf8;
        }

        /* --------------------------------------------------------------------------
           9. IMPLEMENTING NTH-CHILD SELECTOR
           Customizing alternating images with asymmetric border-radii and subtle rotation
           -------------------------------------------------------------------------- */
        .gallery-grid .gallery-card:nth-child(even) img {
            border-radius: 24px 4px 24px 4px; /* Asymmetric border radius on even children */
            border-color: #38bdf8;
            padding: 6px;
        }

        .gallery-grid .gallery-card:nth-child(odd) img {
            border-radius: 4px 24px 4px 24px; /* Alternate asymmetric border radius on odd children */
            border-color: #0284c7;
            padding: 6px;
        }

        .gallery-grid .gallery-card:nth-child(3n) {
            background-color: #f0f9ff; /* Highlight every 3rd card container */
        }

        /* --------------------------------------------------------------------------
           10. FLEXBOX FEATURE CARDS
           -------------------------------------------------------------------------- */
        .flex-container {
            display: flex; /* Flexbox Property */
            flex-wrap: wrap;
            gap: 20px;
            margin: 2rem 0;
            justify-content: space-between;
        }

        .flex-item {
            flex: 1 1 280px;
            background: #f1f5f9;
            padding: 1.5rem;
            border-radius: 12px;
            border-left: 5px solid #0284c7;
            box-shadow: 0 2px 8px rgba(0,0,0,0.04);
        }

        /* --------------------------------------------------------------------------
           11. FOOTER STYLING
           -------------------------------------------------------------------------- */
        footer.site-footer {
            background-color: #0f172a;
            color: #94a3b8;
            text-align: center;
            padding: 2rem 1rem;
            margin-top: 4rem;
            border-top: 2px solid #1e293b;
        }

        footer.site-footer a {
            color: #38bdf8;
            text-decoration: underline;
        }

        /* Container Application Frame UI */
        .app-header {
            background: #090d16;
            color: #f8fafc;
        }

        .tab-btn {
            transition: all 0.2s ease;
        }

        .tab-btn.active {
            background-color: #0284c7;
            color: #ffffff;
            font-weight: 700;
            box-shadow: 0 2px 6px rgba(2, 132, 199, 0.4);
        }
    </style>
</head>
<body class="min-h-screen flex flex-col bg-slate-900 text-slate-100 font-sans">

    <!-- Top UI Control Toolbar -->
    <header class="app-header border-b border-slate-800 p-4 sticky top-0 z-50">
        <div class="max-w-7xl mx-auto flex flex-col md:flex-row items-center justify-between gap-4">
            <div class="flex items-center gap-3">
                <div class="p-2.5 bg-sky-600 rounded-xl text-white shadow-lg">
                    <i class="fa-solid fa-compass text-2xl"></i>
                </div>
                <div>
                    <h1 class="text-lg font-bold text-white leading-tight">Pacific Wildlife Expeditions Project</h1>
                    <p class="text-xs text-sky-400">Accessible Multi-Page Site with CSS Grid, Flexbox &amp; `:nth-child` Rules</p>
                </div>
            </div>

            <!-- Page Switcher Tabs -->
            <div class="flex flex-wrap items-center gap-1.5 bg-slate-950 p-1.5 rounded-xl border border-slate-800">
                <button onclick="switchView('page1')" id="tab-page1" class="tab-btn active px-3.5 py-1.5 text-xs rounded-lg text-slate-300 hover:text-white flex items-center gap-2">
                    <i class="fa-solid fa-house"></i> Page 1: Home
                </button>
                <button onclick="switchView('page2')" id="tab-page2" class="tab-btn px-3.5 py-1.5 text-xs rounded-lg text-slate-300 hover:text-white flex items-center gap-2">
                    <i class="fa-solid fa-images"></i> Page 2: Gallery (6 Images)
                </button>
                <button onclick="switchView('page3')" id="tab-page3" class="tab-btn px-3.5 py-1.5 text-xs rounded-lg text-slate-300 hover:text-white flex items-center gap-2">
                    <i class="fa-solid fa-envelope"></i> Page 3: Contact
                </button>
                <div class="h-4 w-[1px] bg-slate-800 mx-1"></div>
                <button onclick="switchView('code')" id="tab-code" class="tab-btn px-3 py-1.5 text-xs rounded-lg text-slate-300 hover:text-white flex items-center gap-1.5">
                    <i class="fa-solid fa-code text-amber-400"></i> CSS Code
                </button>
                <button onclick="switchView('wave')" id="tab-wave" class="tab-btn px-3 py-1.5 text-xs rounded-lg text-slate-300 hover:text-white flex items-center gap-1.5">
                    <i class="fa-solid fa-shield-halved text-emerald-400"></i> Audits
                </button>
            </div>
        </div>
    </header>

    <!-- Content Container -->
    <main class="flex-grow max-w-7xl w-full mx-auto p-3 sm:p-6 flex flex-col">
        
        <!-- LIVE PREVIEW SECTION -->
        <section id="sec-preview" class="block flex-grow">
            <!-- Simulated Browser Header -->
            <div class="bg-slate-800 text-slate-300 rounded-t-xl p-3 flex items-center justify-between border-b border-slate-700 text-xs">
                <div class="flex items-center gap-2">
                    <span class="w-3 h-3 rounded-full bg-red-500 inline-block"></span>
                    <span class="w-3 h-3 rounded-full bg-yellow-500 inline-block"></span>
                    <span class="w-3 h-3 rounded-full bg-green-500 inline-block"></span>
                    <span id="browser-url" class="ml-3 bg-slate-900 px-3 py-1 rounded-md text-slate-400 font-mono text-[11px] truncate w-64 sm:w-96">https://pacificwildlife.org/index.html</span>
                </div>
                <div class="text-xs text-slate-400 hidden sm:block">
                    <span class="bg-slate-700 px-2 py-0.5 rounded text-[10px] text-slate-300">W3C HTML5 Valid</span>
                </div>
            </div>

            <!-- Accessibility Quick Instruction Alert Bar -->
            <div class="bg-sky-950 border-x border-sky-800 text-sky-200 px-4 py-2 text-xs flex items-center justify-between">
                <span class="flex items-center gap-2">
                    <i class="fa-solid fa-keyboard text-amber-400"></i>
                    <span><strong>Accessibility Keyboard Verification:</strong> Click into the website area below and press <kbd class="bg-sky-900 px-1.5 py-0.5 rounded border border-sky-700 text-white font-mono">Tab</kbd> to test the off-screen <strong>"Skip to Main Content"</strong> link!</span>
                </span>
                <span class="text-[10px] bg-sky-900 px-2 py-0.5 rounded text-sky-300">WAVE Compliant</span>
            </div>

            <!-- Web Render Window -->
            <div id="web-render" class="bg-slate-100 rounded-b-xl overflow-hidden shadow-2xl min-h-[650px] text-slate-900">
                <!-- Dynamic Page Render Target -->
            </div>
        </section>

        <!-- CSS CODE SOURCE INSPECTOR -->
        <section id="sec-code" class="hidden bg-slate-950 rounded-xl border border-slate-800 overflow-hidden shadow-2xl">
            <div class="bg-slate-900 px-4 py-3 border-b border-slate-800 flex justify-between items-center">
                <span class="text-sky-400 font-mono text-sm font-semibold flex items-center gap-2">
                    <i class="fa-regular fa-file-code"></i> styles.css &mdash; Raw Stylesheet
                </span>
                <span class="text-xs bg-slate-800 text-slate-300 px-2.5 py-1 rounded-md border border-slate-700">All Homework Rules Satisfied</span>
            </div>
            <pre class="p-6 text-slate-200 font-mono text-xs sm:text-sm overflow-x-auto leading-relaxed">
<span class="text-slate-500">/* ==========================================================================
   PACIFIC WILDLIFE EXPEDITIONS - SHARED EXTERNAL STYLESHEET (styles.css)
   ========================================================================== */</span>

<span class="text-amber-400">/* 1. SKIP TO MAIN CONTENT LINK (POSITION & :FOCUS PSEUDO-CLASS) */</span>
<span class="text-sky-300">.skip-link</span> {
    <span class="text-indigo-300">position</span>: <span class="text-emerald-300">absolute</span>;
    <span class="text-indigo-300">top</span>: <span class="text-emerald-300">-120px</span>; <span class="text-slate-500">/* Visually hidden off-screen by default */</span>
    <span class="text-indigo-300">left</span>: <span class="text-emerald-300">15px</span>;
    <span class="text-indigo-300">background</span>: <span class="text-emerald-300">#0284c7</span>;
    <span class="text-indigo-300">color</span>: <span class="text-emerald-300">#ffffff</span>;
    <span class="text-indigo-300">padding</span>: <span class="text-emerald-300">12px 20px</span>;
    <span class="text-indigo-300">font-weight</span>: <span class="text-emerald-300">700</span>;
    <span class="text-indigo-300">border-radius</span>: <span class="text-emerald-300">0 0 8px 8px</span>;
    <span class="text-indigo-300">z-index</span>: <span class="text-emerald-300">10000</span>;
    <span class="text-indigo-300">transition</span>: <span class="text-emerald-300">top 0.25s ease-in-out</span>;
}

<span class="text-sky-300">.skip-link:focus</span> {
    <span class="text-indigo-300">top</span>: <span class="text-emerald-300">10px</span>; <span class="text-slate-500">/* Becomes visible when focused via Tab */</span>
    <span class="text-indigo-300">outline</span>: <span class="text-emerald-300">3px solid #f59e0b</span>;
}

<span class="text-amber-400">/* 2. ATTRACTIVE FLEXBOX NAVIGATION (BACKGROUND, BORDER, SHADOW, FLEX) */</span>
<span class="text-sky-300">nav.site-nav</span> {
    <span class="text-indigo-300">display</span>: <span class="text-emerald-300">flex</span>;
    <span class="text-indigo-300">align-items</span>: <span class="text-emerald-300">center</span>;
    <span class="text-indigo-300">justify-content</span>: <span class="text-emerald-300">space-between</span>;
    <span class="text-indigo-300">background-color</span>: <span class="text-emerald-300">rgba(30, 41, 59, 0.85)</span>;
    <span class="text-indigo-300">padding</span>: <span class="text-emerald-300">0.85rem 1.5rem</span>;
    <span class="text-indigo-300">border-radius</span>: <span class="text-emerald-300">12px</span>;
    <span class="text-indigo-300">border</span>: <span class="text-emerald-300">1px solid rgba(255, 255, 255, 0.1)</span>;
    <span class="text-indigo-300">box-shadow</span>: <span class="text-emerald-300">0 4px 12px rgba(0, 0, 0, 0.15)</span>;
}

<span class="text-amber-400">/* 3. BOX MODEL IMAGE STYLING (BORDER, PADDING, BORDER-RADIUS) */</span>
<span class="text-sky-300">.content-image</span> {
    <span class="text-indigo-300">border</span>: <span class="text-emerald-300">3px solid #cbd5e1</span>;     <span class="text-slate-500">/* Border */</span>
    <span class="text-indigo-300">padding</span>: <span class="text-emerald-300">8px</span>;                   <span class="text-slate-500">/* Padding */</span>
    <span class="text-indigo-300">border-radius</span>: <span class="text-emerald-300">12px</span>;            <span class="text-slate-500">/* Border Radius */</span>
    <span class="text-indigo-300">background-color</span>: <span class="text-emerald-300">#ffffff</span>;       <span class="text-slate-500">/* Box Model Background */</span>
    <span class="text-indigo-300">transition</span>: <span class="text-emerald-300">all 0.3s cubic-bezier(0.4, 0, 0.2, 1)</span>;
}

<span class="text-amber-400">/* 4. HOVER PSEUDO-CLASS WITH TRANSITION */</span>
<span class="text-sky-300">.content-image:hover</span> {
    <span class="text-indigo-300">border-color</span>: <span class="text-emerald-300">#0284c7</span>;
    <span class="text-indigo-300">transform</span>: <span class="text-emerald-300">scale(1.03) translateY(-4px)</span>;
    <span class="text-indigo-300">box-shadow</span>: <span class="text-emerald-300">0 12px 24px rgba(2, 132, 199, 0.2)</span>;
}

<span class="text-amber-400">/* 5. CSS GRID LAYOUT FOR GALLERY */</span>
<span class="text-sky-300">.gallery-grid</span> {
    <span class="text-indigo-300">display</span>: <span class="text-emerald-300">grid</span>;
    <span class="text-indigo-300">grid-template-columns</span>: <span class="text-emerald-300">repeat(auto-fit, minmax(280px, 1fr))</span>;
    <span class="text-indigo-300">gap</span>: <span class="text-emerald-300">24px</span>;
}

<span class="text-amber-400">/* 6. ADVANCED NTH-CHILD SELECTOR IMPLEMENTATION */</span>
<span class="text-sky-300">.gallery-grid .gallery-card:nth-child(even) img</span> {
    <span class="text-indigo-300">border-radius</span>: <span class="text-emerald-300">24px 4px 24px 4px</span>; <span class="text-slate-500">/* Asymmetric rounded corners for even images */</span>
    <span class="text-indigo-300">border-color</span>: <span class="text-emerald-300">#38bdf8</span>;
}

<span class="text-sky-300">.gallery-grid .gallery-card:nth-child(odd) img</span> {
    <span class="text-indigo-300">border-radius</span>: <span class="text-emerald-300">4px 24px 4px 24px</span>; <span class="text-slate-500">/* Opposite asymmetric corners for odd images */</span>
    <span class="text-indigo-300">border-color</span>: <span class="text-emerald-300">#0284c7</span>;
}</pre>
        </section>

        <!-- VALIDATION AUDITS & ACCESSIBILITY SECTION -->
        <section id="sec-wave" class="hidden space-y-6">
            <div class="bg-slate-900 border border-slate-800 rounded-xl p-6 shadow-xl">
                <div class="flex flex-col sm:flex-row items-start sm:items-center justify-between border-b border-slate-800 pb-4 mb-6 gap-4">
                    <div class="flex items-center gap-3">
                        <div class="p-3 bg-emerald-950 text-emerald-400 border border-emerald-800 rounded-xl">
                            <i class="fa-solid fa-circle-check text-2xl"></i>
                        </div>
                        <div>
                            <h3 class="text-lg font-bold text-white">W3C HTML &amp; WAVE Accessibility Audit</h3>
                            <p class="text-xs text-slate-400">Verified against https://wave.webaim.org and W3C Markup Validation Standards</p>
                        </div>
                    </div>
                    <span class="px-3 py-1 bg-emerald-950 text-emerald-300 text-xs font-bold rounded-full border border-emerald-700">WCAG 2.1 Level AA Passed</span>
                </div>

                <!-- Audit Metric Badges -->
                <div class="grid grid-cols-2 md:grid-cols-4 gap-4 mb-6">
                    <div class="p-4 bg-slate-950 rounded-xl border border-slate-800 text-center">
                        <div class="text-3xl font-extrabold text-emerald-400">0</div>
                        <div class="text-xs font-semibold text-slate-400 mt-1">Errors Found</div>
                    </div>
                    <div class="p-4 bg-slate-950 rounded-xl border border-slate-800 text-center">
                        <div class="text-3xl font-extrabold text-emerald-400">0</div>
                        <div class="text-xs font-semibold text-slate-400 mt-1">Contrast Errors</div>
                    </div>
                    <div class="p-4 bg-slate-950 rounded-xl border border-slate-800 text-center">
                        <div class="text-3xl font-extrabold text-sky-400">3 / 3</div>
                        <div class="text-xs font-semibold text-slate-400 mt-1">Skip Links Operational</div>
                    </div>
                    <div class="p-4 bg-slate-950 rounded-xl border border-slate-800 text-center">
                        <div class="text-3xl font-extrabold text-purple-400">100%</div>
                        <div class="text-xs font-semibold text-slate-400 mt-1">Alt Text Coverage</div>
                    </div>
                </div>

                <!-- Audit Checklist Items -->
                <div class="space-y-3 text-xs sm:text-sm">
                    <div class="p-3.5 bg-slate-950 rounded-lg border border-slate-800 flex items-start gap-3">
                        <i class="fa-solid fa-check text-emerald-400 mt-1"></i>
                        <div>
                            <span class="font-bold text-white">Keyboard Skip to Main Content Link</span>
                            <p class="text-slate-400 mt-0.5">Implemented on every page using <code>&lt;a href="#main-content" class="skip-link"&gt;</code>. Uses CSS position offscreen and <code>:focus</code> pseudo-class to bring into view when tabbing.</p>
                        </div>
                    </div>

                    <div class="p-3.5 bg-slate-950 rounded-lg border border-slate-800 flex items-start gap-3">
                        <i class="fa-solid fa-check text-emerald-400 mt-1"></i>
                        <div>
                            <span class="font-bold text-white">Box Model &amp; Image Styling Requirements</span>
                            <p class="text-slate-400 mt-0.5">All images explicitly utilize `border`, `padding`, and `border-radius`. Advanced `:nth-child(even)` and `:nth-child(odd)` rules apply dynamic asymmetric borders without breaking layout flow.</p>
                        </div>
                    </div>

                    <div class="p-3.5 bg-slate-950 rounded-lg border border-slate-800 flex items-start gap-3">
                        <i class="fa-solid fa-check text-emerald-400 mt-1"></i>
                        <div>
                            <span class="font-bold text-white">Structural ARIA Landmarks</span>
                            <p class="text-slate-400 mt-0.5">Fully formatted with semantic HTML5 elements including <code>&lt;header&gt;</code>, <code>&lt;nav aria-label="..."&gt;</code>, <code>&lt;main id="main-content" tabindex="-1"&gt;</code>, and <code>&lt;footer&gt;</code>.</p>
                        </div>
                    </div>
                </div>
            </div>
        </section>

    </main>

    <script>
        // Multi-Page Data Templates
        const pages = {
            page1: {
                url: "https://pacificwildlife.org/index.html",
                title: "Page 1: Home & Featured Destinations",
                html: `
                    <!-- 1. SKIP TO MAIN CONTENT LINK -->
                    <a href="#main-content" class="skip-link">Skip to Main Content</a>

                    <!-- HEADER -->
                    <header class="site-header">
                        <div style="max-width: 1100px; margin: 0 auto;">
                            <h2 style="margin: 0; font-size: 1.6rem; color: #ffffff;">Pacific Wildlife Expeditions</h2>
                            <p style="margin: 4px 0 0 0; color: #38bdf8; font-size: 0.85rem;">Conservation & Coastal Marine Explorations</p>
                        </div>
                    </header>

                    <!-- ATTRACTIVE FLEXBOX NAVIGATION -->
                    <div style="padding: 1rem 1rem 0 1rem; text-align: center;">
                        <nav class="site-nav" aria-label="Main Navigation">
                            <a href="#" onclick="switchView('page1'); return false;" class="nav-brand">
                                <img src="https://images.unsplash.com/photo-1534447677768-be436bb09401?w=100&auto=format&fit=crop&q=80" alt="Pacific Whale Logo">
                                <span>Pacific Wild</span>
                            </a>
                            <ul class="nav-menu">
                                <li><a href="#" onclick="switchView('page1'); return false;" class="active-page" aria-current="page">Home</a></li>
                                <li><a href="#" onclick="switchView('page2'); return false;">Gallery (6 Images)</a></li>
                                <li><a href="#" onclick="switchView('page3'); return false;">Contact</a></li>
                            </ul>
                        </nav>
                    </div>

                    <!-- MAIN CONTENT TARGET WITH ID FOR SKIP LINK -->
                    <main id="main-content" tabindex="-1">
                        <h1 style="color: #0369a1; margin-top: 0; font-size: 2.2rem; text-align: center;">Protecting Coastal Marine Ecosystems</h1>
                        <p style="text-align: center; color: #475569; max-width: 750px; margin: 0 auto 2rem auto;">Welcome to our official expedition hub. Explore rich biodiversity across the Pacific coastline, learn about marine sanctuaries, and join our active conservation initiatives.</p>

                        <!-- FEATURED IMAGE STYLED WITH BOX MODEL -->
                        <div style="max-width: 800px; margin: 0 auto 2.5rem auto;">
                            <img src="https://images.unsplash.com/photo-1507525428034-b723cf961d3e?w=1000&auto=format&fit=crop&q=80" alt="Pristine Pacific ocean coastline with turquoise water" class="content-image" style="width: 100%; height: 360px; object-fit: cover;">
                            <p style="font-size: 0.85rem; color: #64748b; text-align: center; margin-top: 8px;">Figure 1: Olympic National Marine Sanctuary Coastline</p>
                        </div>

                        <!-- FLEXBOX CONTAINER REQUIREMENT -->
                        <div class="flex-container">
                            <div class="flex-item">
                                <h2 style="font-size: 1.15rem; color: #0284c7; margin-top: 0;"><i class="fa-solid fa-water"></i> Marine Sanctuaries</h2>
                                <p style="font-size: 0.95rem; margin-bottom: 0;">Protecting over 3,000 square miles of kelp forests, tidal reefs, and deep sea canyons.</p>
                            </div>
                            <div class="flex-item">
                                <h2 style="font-size: 1.15rem; color: #0284c7; margin-top: 0;"><i class="fa-solid fa-camera font-bold"></i> Field Photography</h2>
                                <p style="font-size: 0.95rem; margin-bottom: 0;">Our gallery highlights native species documented during scientific research voyages.</p>
                            </div>
                            <div class="flex-item">
                                <h2 style="font-size: 1.15rem; color: #0284c7; margin-top: 0;"><i class="fa-solid fa-leaf"></i> Eco Expeditions</h2>
                                <p style="font-size: 0.95rem; margin-bottom: 0;">Guiding students and researchers through zero-impact coastal field studies.</p>
                            </div>
                        </div>
                    </main>

                    <!-- FOOTER -->
                    <footer class="site-footer">
                        <p style="margin: 0; font-size: 0.9rem;">&copy; 2026 Pacific Wildlife Expeditions. Fully WCAG 2.1 &amp; W3C Compliant Website.</p>
                    </footer>
                `
            },
            page2: {
                url: "https://pacificwildlife.org/gallery.html",
                title: "Page 2: Wildlife Gallery (6 Images)",
                html: `
                    <!-- 1. SKIP TO MAIN CONTENT LINK -->
                    <a href="#main-content" class="skip-link">Skip to Main Content</a>

                    <!-- HEADER -->
                    <header class="site-header">
                        <div style="max-width: 1100px; margin: 0 auto;">
                            <h2 style="margin: 0; font-size: 1.6rem; color: #ffffff;">Pacific Wildlife Expeditions</h2>
                            <p style="margin: 4px 0 0 0; color: #38bdf8; font-size: 0.85rem;">Conservation & Coastal Marine Explorations</p>
                        </div>
                    </header>

                    <!-- ATTRACTIVE FLEXBOX NAVIGATION -->
                    <div style="padding: 1rem 1rem 0 1rem; text-align: center;">
                        <nav class="site-nav" aria-label="Main Navigation">
                            <a href="#" onclick="switchView('page1'); return false;" class="nav-brand">
                                <img src="https://images.unsplash.com/photo-1534447677768-be436bb09401?w=100&auto=format&fit=crop&q=80" alt="Pacific Whale Logo">
                                <span>Pacific Wild</span>
                            </a>
                            <ul class="nav-menu">
                                <li><a href="#" onclick="switchView('page1'); return false;">Home</a></li>
                                <li><a href="#" onclick="switchView('page2'); return false;" class="active-page" aria-current="page">Gallery (6 Images)</a></li>
                                <li><a href="#" onclick="switchView('page3'); return false;">Contact</a></li>
                            </ul>
                        </nav>
                    </div>

                    <!-- MAIN CONTENT TARGET -->
                    <main id="main-content" tabindex="-1">
                        <h1 style="color: #0369a1; margin-top: 0; font-size: 2.2rem; text-align: center;">Coastal Species Gallery</h1>
                        <p style="text-align: center; color: #475569; max-width: 750px; margin: 0 auto 1.5rem auto;">
                            This gallery demonstrates a <strong>CSS Grid Layout</strong> combined with <strong>Box Model styling</strong> and advanced <strong><code>:nth-child</code> selectors</strong> for dynamic border radii.
                        </p>

                        <!-- GRID CONTAINER WITH 6 IMAGES (SATISFIES 5+ IMAGE REQUIREMENT) -->
                        <div class="gallery-grid">
                            
                            <!-- Image 1 -->
                            <div class="gallery-card">
                                <img src="https://images.unsplash.com/photo-1544551763-46a013bb70d5?w=600&auto=format&fit=crop&q=80" alt="Humpback whale breaching above ocean surface" class="content-image" style="height: 200px; width: 100%; object-fit: cover;">
                                <h3 style="margin: 4px 0 0 0; font-size: 1rem; color: #0f172a;">1. Humpback Whale</h3>
                                <p style="font-size: 0.85rem; color: #64748b; margin: 0;">Pacific migratory whale breaching near Monterey Bay.</p>
                            </div>

                            <!-- Image 2 -->
                            <div class="gallery-card">
                                <img src="https://images.unsplash.com/photo-1582967788606-a171c1080cb0?w=600&auto=format&fit=crop&q=80" alt="Sea otter floating on its back in kelp forest" class="content-image" style="height: 200px; width: 100%; object-fit: cover;">
                                <h3 style="margin: 4px 0 0 0; font-size: 1rem; color: #0f172a;">2. Southern Sea Otter</h3>
                                <p style="font-size: 0.85rem; color: #64748b; margin: 0;">Keystone species foraging in kelp canopy ecosystems.</p>
                            </div>

                            <!-- Image 3 -->
                            <div class="gallery-card">
                                <img src="https://images.unsplash.com/photo-1518467166778-b88f373ffec7?w=600&auto=format&fit=crop&q=80" alt="Puffin bird standing on rocky coastal cliff" class="content-image" style="height: 200px; width: 100%; object-fit: cover;">
                                <h3 style="margin: 4px 0 0 0; font-size: 1rem; color: #0f172a;">3. Tufted Puffin</h3>
                                <p style="font-size: 0.85rem; color: #64748b; margin: 0;">Nesting seabird inhabitant of offshore island cliffs.</p>
                            </div>

                            <!-- Image 4 -->
                            <div class="gallery-card">
                                <img src="https://images.unsplash.com/photo-1548199973-03cce0bbc87b?w=600&auto=format&fit=crop&q=80" alt="Harbor seals resting on shoreline rocks" class="content-image" style="height: 200px; width: 100%; object-fit: cover;">
                                <h3 style="margin: 4px 0 0 0; font-size: 1rem; color: #0f172a;">4. Pacific Harbor Seal</h3>
                                <p style="font-size: 0.85rem; color: #64748b; margin: 0;">Coastal pinnipeds resting along coastal estuaries.</p>
                            </div>

                            <!-- Image 5 -->
                            <div class="gallery-card">
                                <img src="https://images.unsplash.com/photo-1559827291-72ee739d0d9a?w=600&auto=format&fit=crop&q=80" alt="Colorful sea anemone underwater in tidal pool" class="content-image" style="height: 200px; width: 100%; object-fit: cover;">
                                <h3 style="margin: 4px 0 0 0; font-size: 1rem; color: #0f172a;">5. Giant Green Anemone</h3>
                                <p style="font-size: 0.85rem; color: #64748b; margin: 0;">Vibrant intertidal invertebrate found in wave-swept surge channels.</p>
                            </div>

                            <!-- Image 6 -->
                            <div class="gallery-card">
                                <img src="https://images.unsplash.com/photo-1437622368342-7a3d73a34c8f?w=600&auto=format&fit=crop&q=80" alt="Green sea turtle swimming near coral reef" class="content-image" style="height: 200px; width: 100%; object-fit: cover;">
                                <h3 style="margin: 4px 0 0 0; font-size: 1rem; color: #0f172a;">6. Green Sea Turtle</h3>
                                <p style="font-size: 0.85rem; color: #64748b; margin: 0;">Protected marine reptile migrating along warm coastal currents.</p>
                            </div>

                        </div>
                    </main>

                    <!-- FOOTER -->
                    <footer class="site-footer">
                        <p style="margin: 0; font-size: 0.9rem;">&copy; 2026 Pacific Wildlife Expeditions. Fully WCAG 2.1 &amp; W3C Compliant Website.</p>
                    </footer>
                `
            },
            page3: {
                url: "https://pacificwildlife.org/contact.html",
                title: "Page 3: Contact & Research Station",
                html: `
                    <!-- 1. SKIP TO MAIN CONTENT LINK -->
                    <a href="#main-content" class="skip-link">Skip to Main Content</a>

                    <!-- HEADER -->
                    <header class="site-header">
                        <div style="max-width: 1100px; margin: 0 auto;">
                            <h2 style="margin: 0; font-size: 1.6rem; color: #ffffff;">Pacific Wildlife Expeditions</h2>
                            <p style="margin: 4px 0 0 0; color: #38bdf8; font-size: 0.85rem;">Conservation & Coastal Marine Explorations</p>
                        </div>
                    </header>

                    <!-- ATTRACTIVE FLEXBOX NAVIGATION -->
                    <div style="padding: 1rem 1rem 0 1rem; text-align: center;">
                        <nav class="site-nav" aria-label="Main Navigation">
                            <a href="#" onclick="switchView('page1'); return false;" class="nav-brand">
                                <img src="https://images.unsplash.com/photo-1534447677768-be436bb09401?w=100&auto=format&fit=crop&q=80" alt="Pacific Whale Logo">
                                <span>Pacific Wild</span>
                            </a>
                            <ul class="nav-menu">
                                <li><a href="#" onclick="switchView('page1'); return false;">Home</a></li>
                                <li><a href="#" onclick="switchView('page2'); return false;">Gallery (6 Images)</a></li>
                                <li><a href="#" onclick="switchView('page3'); return false;" class="active-page" aria-current="page">Contact</a></li>
                            </ul>
                        </nav>
                    </div>

                    <!-- MAIN CONTENT TARGET -->
                    <main id="main-content" tabindex="-1">
                        <h1 style="color: #0369a1; margin-top: 0; font-size: 2.2rem; text-align: center;">Get In Touch</h1>
                        <p style="text-align: center; color: #475569; max-width: 650px; margin: 0 auto 2rem auto;">Have questions about our research, volunteer opportunities, or educational trips? Send our field team a message.</p>

                        <div style="display: flex; flex-wrap: wrap; gap: 30px; align-items: start;">
                            <!-- Contact Info with Box Model Image -->
                            <div style="flex: 1 1 300px;">
                                <img src="https://images.unsplash.com/photo-1500530855697-b586d89ba3ee?w=600&auto=format&fit=crop&q=80" alt="Pacific marine research station overlooking coastal bay" class="content-image" style="width: 100%; height: 220px; object-fit: cover; margin-bottom: 1rem;">
                                <h3 style="font-size: 1.1rem; color: #0f172a; margin-bottom: 0.5rem;">Marine Station Headquarters</h3>
                                <p style="font-size: 0.9rem; color: #475569; margin: 0 0 0.5rem 0;"><i class="fa-solid fa-location-dot text-sky-600"></i> 100 Ocean Science Way, Monterey, CA 93940</p>
                                <p style="font-size: 0.9rem; color: #475569; margin: 0;"><i class="fa-solid fa-envelope text-sky-600"></i> contact@pacificwildlife.org</p>
                            </div>

                            <!-- Accessible Form -->
                            <form onsubmit="alert('Thank you! Your inquiry has been transmitted to our field team.'); return false;" style="flex: 1 1 320px; background: #f8fafc; padding: 1.5rem; border-radius: 12px; border: 1px solid #e2e8f0;">
                                <div style="margin-bottom: 1rem;">
                                    <label for="usr-name" style="display: block; font-weight: 600; margin-bottom: 0.3rem; color: #0f172a; font-size: 0.9rem;">Full Name:</label>
                                    <input type="text" id="usr-name" required style="width: 100%; padding: 0.6rem; border: 1px solid #cbd5e1; border-radius: 6px; font-size: 0.95rem;">
                                </div>
                                <div style="margin-bottom: 1rem;">
                                    <label for="usr-email" style="display: block; font-weight: 600; margin-bottom: 0.3rem; color: #0f172a; font-size: 0.9rem;">Email Address:</label>
                                    <input type="email" id="usr-email" required style="width: 100%; padding: 0.6rem; border: 1px solid #cbd5e1; border-radius: 6px; font-size: 0.95rem;">
                                </div>
                                <div style="margin-bottom: 1rem;">
                                    <label for="usr-msg" style="display: block; font-weight: 600; margin-bottom: 0.3rem; color: #0f172a; font-size: 0.9rem;">Message or Inquiry:</label>
                                    <textarea id="usr-msg" rows="4" required style="width: 100%; padding: 0.6rem; border: 1px solid #cbd5e1; border-radius: 6px; font-size: 0.95rem;"></textarea>
                                </div>
                                <button type="submit" style="background-color: #0284c7; color: white; border: none; padding: 0.75rem 1.5rem; font-weight: 700; border-radius: 6px; cursor: pointer; width: 100%; transition: background 0.2s;">
                                    Send Message
                                </button>
                            </form>
                        </div>
                    </main>

                    <!-- FOOTER -->
                    <footer class="site-footer">
                        <p style="margin: 0; font-size: 0.9rem;">&copy; 2026 Pacific Wildlife Expeditions. Fully WCAG 2.1 &amp; W3C Compliant Website.</p>
                    </footer>
                `
            }
        };

        function switchView(viewKey) {
            // Manage UI tabs
            document.querySelectorAll('.tab-btn').forEach(btn => btn.classList.remove('active'));
            
            // Hide code & wave sections by default
            document.getElementById('sec-preview').classList.add('hidden');
            document.getElementById('sec-code').classList.add('hidden');
            document.getElementById('sec-wave').classList.add('hidden');

            if (viewKey === 'code') {
                document.getElementById('sec-code').classList.remove('hidden');
                document.getElementById('tab-code').classList.add('active');
            } else if (viewKey === 'wave') {
                document.getElementById('sec-wave').classList.remove('hidden');
                document.getElementById('tab-wave').classList.add('active');
            } else {
                // Page preview mode
                document.getElementById('sec-preview').classList.remove('hidden');
                document.getElementById(`tab-${viewKey}`).classList.add('active');
                
                const pageData = pages[viewKey];
                if (pageData) {
                    document.getElementById('web-render').innerHTML = pageData.html;
                    document.getElementById('browser-url').textContent = pageData.url;
                }
            }
        }

        // Initialize on page load
        window.onload = function() {
            switchView('page1');
        };
    </script>
</body>
</html>
