# Acadrez — Pakistani University Aggregate Calculator

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Deployed on Cloudflare Pages](https://img.shields.io/badge/Deployed_on-Cloudflare_Pages-F38020?logo=cloudflare)](https://acadrez.pages.dev)
[![HTML5](https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white)](#)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-38B2AC?logo=tailwind-css&logoColor=white)](#)

> **Acadrez** (formerly Acadify) is a free, fast, and 100% client-side aggregate calculator built for students applying to top Pakistani universities. 

🌐 **Live Website:** [https://acadrez.pages.dev](https://acadrez.pages.dev)

---

## 📖 About The Project

Every year, thousands of Pakistani students struggle with calculating their merit aggregates for university admissions. Formulas vary wildly between NUST, FAST, UET, COMSATS, GIKI, and others. **Acadrez** solves this by providing a single, unified interface that instantly calculates aggregates based on the latest official prospectuses.

### Key Features
- **⏳ Lightning Fast:** Calculates results instantly in under 60 seconds.
- **📚 15+ Universities:** Preset formulas for FAST, NUST, UET, COMSATS, PIEAS, NED, GIKI, Air University, and more.
- **🔒 Privacy First:** 100% client-side. No login, no ads, no cookies, no tracking. Your marks never leave your browser.
- **📱 Mobile Optimized:** Designed as a responsive, app-like experience for phones and tablets.
- **🔗 Shareable:** Integrated Web Share API to easily copy or share links to the calculator.
- **✏️ Manual Mode:** Allows users to calculate custom weights if their university isn't in the preset list.

---

## 🛠 Tech Stack

Acadrez is built for speed and simplicity. There is **no backend, no database, no build step, and no framework.** 

- **Frontend Core:** Vanilla HTML5, CSS3, JavaScript (ES6+).
- **Styling:** [Tailwind CSS (via CDN)](https://tailwindcss.com/) for rapid styling across mobile and desktop.
- **Icons & Fonts:** Google Fonts (Lexend, Inter) and Google Material Symbols.
- **Hosting / CI:** Cloudflare Pages (auto-deployed via GitHub).

---

## 📂 File Structure

```text
├── index.html            # Main calculator application
├── about.html            # About the project & mission
├── how-it-works.html     # Guide to manual aggregate calculation
├── universities.html     # Directory of supported universities
├── 404.html              # Custom 404 error page 
├── Universities.js       # Core logic: formula dataset + search logic (Included in HTML pages)
├── robots.txt            # SEO crawler rules
├── sitemap.xml           # XML sitemap for SEO
└── README.md             # Project documentation (You are here)
```

---

## 💻 Local Development

Because Acadrez is entirely static, there's no complex build config or dependencies to install.

1. **Clone the repo:**
   ```bash
   git clone https://github.com/yourusername/acadrez-calculator.git
   cd acadrez-calculator
   ```

2. **Run a local server:**
   You can use any local static web server to avoid CORS issues when standard scripts run. If you have Python installed:
   ```bash
   python -m http.server 8000
   ```
   Or using Node.js:
   ```bash
   npx serve .
   ```

3. **Open in browser:**
   Navigate to `http://localhost:8000` (or the port provided by your server).

---

## 🤝 Contributing

University formulas change every year. Contributions from the open-source community to update formulas or add new universities are highly encouraged.

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AddNewUniversity`)
3. Update `Universities.js` with the new university formulas.
4. Update `universities.html` JSON-LD data.
5. Commit your Changes (`git commit -m 'Add: FAST NU 2026 formula'`)
6. Push to the Branch (`git push origin feature/AddNewUniversity`)
7. Open a Pull Request

---

## 📝 License

Distributed under the MIT License. You are free to use, modify, and distribute this project. See `LICENSE` for more information.

---

## 📫 Contact & Support

**Project Link:** [https://acadrez.pages.dev](https://acadrez.pages.dev)

Issues and bug reports can be submitted on the [GitHub Issues](https://github.com/yourusername/acadrez-calculator/issues) page.
