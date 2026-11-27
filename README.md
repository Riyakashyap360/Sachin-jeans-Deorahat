# Sachin-jeans-Deorahat
Cloths furniture and electronics shop websites design 
sachin-jeans-furniture/
├── .github/
│   └── workflows/
│       └── deploy.yml
├── public/
│   ├── _redirects
│   ├── business-config.json
│   └── assets/
│       └── aistudio/
│           └── Screenshot_2026_1113_115602_2a6be01e.png   (Brand logo image)
├── src/
│   ├── assets/
│   │   └── images/
│   │       ├── hero_showroom_interior_1794551335043.jpg
│   │       ├── cat_mens_fashion_1794551335253.jpg
│   │       ├── cat_womens_fashion_1794551335354.jpg
│   │       ├── cat_watches_1794551336180.jpg
│   │       ├── cat_perfumes_1794551336001.jpg
│   │       ├── cat_accessories_1794551337004.jpg
│   │       ├── cat_furniture_1794551336508.jpg
│   │       └── cat_electronics_1794551338094.jpg
│   ├── components/
│   │   ├── Footer.tsx
│   │   ├── Header.tsx
│   │   ├── ImageWithFallback.tsx
│   │   ├── ProductCard.tsx
│   │   ├── ProductModal.tsx
│   │   └── StoreSettingsModal.tsx
│   ├── config/
│   │   └── businessConfig.ts
│   ├── data/
│   │   ├── catalogue.ts
│   │   └── media.ts
│   ├── pages/
│   │   ├── AboutPage.tsx
│   │   ├── CategoryPage.tsx
│   │   ├── ContactPage.tsx
│   │   └── HomePage.tsx
│   ├── utils/
│   │   ├── catalogueLogic.ts
│   │   ├── retailLogic.test.ts
│   │   └── whatsapp.ts
│   ├── App.tsx
│   ├── index.css
│   └── main.tsx
├── .gitignore
├── index.html
├── package.json
├── README.md
├── tsconfig.json
├── vercel.json
└── vite.config.ts
name: Deploy to GitHub Pages

on:
  push:
    branches:
      - main
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: pages
  cancel-in-progress: false

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: 20
          cache: npm

      - name: Install dependencies
        run: npm ci

      - name: Type-check & run tests
        run: |
          npm run lint
          npm test

      - name: Build for GitHub Pages
        env:
          REPO_NAME: ${{ github.event.repository.name }}
        run: |
          if [ -f public/CNAME ]; then
            export VITE_BASE_PATH="/"
          else
            export VITE_BASE_PATH="/${REPO_NAME}/"
          fi
          npm run build
          cp dist/index.html dist/404.html

      - name: Setup GitHub Pages
        uses: actions/configure-pages@v5

      - name: Upload Pages artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: dist

  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
        {
  "name": "sachin-jeans-furniture",
  "private": true,
  "version": "1.0.0",
  "type": "module",
  "scripts": {
    "dev": "vite --port=3000 --host=0.0.0.0",
    "build": "vite build",
    "preview": "vite preview",
    "clean": "rm -rf dist server.js",
    "lint": "tsc --noEmit",
    "test": "tsx --test src/utils/retailLogic.test.ts"
  },
  "dependencies": {
    "@google/genai": "^2.4.0",
    "@tailwindcss/vite": "^4.3.3",
    "@vitejs/plugin-react": "^6.1.1",
    "lucide-react": "^0.546.0",
    "react": "^19.0.1",
    "react-dom": "^19.0.1",
    "vite": "^8.3.0",
    "express": "^4.21.2",
    "dotenv": "^17.2.3",
    "motion": "^12.23.24"
  },
  "devDependencies": {
    "@types/node": "^22.14.0",
    "@types/react": "^19.3.0",
    "@types/react-dom": "^19.3.0",
    "autoprefixer": "^10.4.21",
    "esbuild": "^0.25.0",
    "tailwindcss": "^4.3.3",
    "tsx": "^4.21.0",
    "typescript": "^7.0.2",
    "@types/express": "^4.17.21"
  }
}
import tailwindcss from '@tailwindcss/vite';
import react from '@vitejs/plugin-react';
import path from 'path';
import {defineConfig} from 'vite';

export default defineConfig(() => {
  return {
    base: process.env.VITE_BASE_PATH || '/',
    plugins: [react(), tailwindcss()],
    resolve: {
      alias: {
        '@': path.resolve(__dirname, '.'),
      },
    },
    server: {
      // HMR is disabled in AI Studio via DISABLE_HMR env var.
      // Do not modify—file watching is disabled to prevent flickering during agent edits.
      hmr: process.env.DISABLE_HMR !== 'true',
      // Disable file watching when DISABLE_HMR is true to save CPU during agent edits.
      watch: process.env.DISABLE_HMR === 'true' ? null : {},
    },
  };
});
{
  "compilerOptions": {
    "target": "ES2022",
    "experimentalDecorators": true,
    "useDefineForClassFields": false,
    "module": "ESNext",
    "types": ["vite/client"],
    "lib": [
      "ES2022",
      "DOM",
      "DOM.Iterable"
    ],
    "skipLibCheck": true,
    "moduleResolution": "bundler",
    "isolatedModules": true,
    "moduleDetection": "force",
    "allowJs": true,
    "jsx": "react-jsx",
    "paths": {
      "@/*": [
        "./*"
      ]
    },
    "allowImportingTsExtensions": true,
    "noEmit": true
  },
  "exclude": ["dist"]
}
{
  "rewrites": [
    { "source": "/(.*)", "destination": "/index.html" }
  ]
}
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Sachin Jeans &amp; Furniture – Multi-Category Retail Showroom</title>
    <meta
      name="description"
      content="Explore men's and women's fashion, watches, perfumes, accessories, furniture, and electronics under one roof at Sachin Jeans & Furniture."
    />
    <meta property="og:title" content="Sachin Jeans & Furniture – Multi-Category Retail Showroom" />
    <meta
      property="og:description"
      content="Explore men's and women's fashion, watches, perfumes, accessories, furniture, and electronics under one roof at Sachin Jeans & Furniture."
    />
    <meta property="og:type" content="website" />
    <meta property="og:site_name" content="Sachin Jeans & Furniture" />
    <meta name="twitter:card" content="summary_large_image" />
    <meta name="twitter:title" content="Sachin Jeans & Furniture – Multi-Category Retail Showroom" />
    <meta
      name="twitter:description"
      content="Multi-category retail showroom offering curated apparel, watches, fragrances, accessories, furniture, and electronics from established brands."
    />
    <link rel="preconnect" href="https://fonts.googleapis.com" />
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
    <link
      href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,500;0,600;0,700;1,500&family=Plus+Jakarta+Sans:wght@400;500;600;700&display=swap"
      rel="stylesheet"
    />
    <script type="application/ld+json">
      {
        "@context": "https://schema.org",
        "@type": "DepartmentStore",
        "name": "Sachin Jeans & Furniture",
        "description": "Multi-category retail showroom selling men's and women's fashion, watches, perfumes, fashion accessories, furniture, and electronics from multiple established brands.",
        "telephone": "+91-62680-57508",
        "address": {
          "@type": "PostalAddress",
          "streetAddress": "Gol Bazar, Devarhat",
          "addressLocality": "Devarhat",
          "addressCountry": "IN"
        }
      }
    </script>
  </head>
  <body class="bg-[#FAF8F5] text-[#1B1917] antialiased selection:bg-[#C49B54]/25 selection:text-[#1B1917]">
    <div id="root"></div>
    <script type="module" src="/src/main.tsx"></script>
  </body>
</html>
# Sachin Jeans & Furniture — Multi-Category Retail Showroom Website

A complete, responsive, multi-page retail showroom web application built with React, TypeScript, Vite, and Tailwind CSS. Designed for portability so the business owner can host it on any free static hosting account and attach a custom domain.

---

## 1. Central Business Configuration (No Code Edits Required)

All showroom contact details are managed centrally in **`public/business-config.json`** (loaded automatically at runtime) with TypeScript defaults in **`src/config/businessConfig.ts`**:

- **Contact Phone Number (`phoneDisplay`)**: `+91 62680 57508`
- **WhatsApp Number (`whatsappNumber`)**: `916268057508`
- **Address (`addressLine1`, `addressLine2`)**: `Gol Bazar, Devarhat` (`गोल बाजार, देवरहट`)
- **Google Maps Query (`mapQuery`)**: `Gol Bazar, Devarhat`
- **Email (`email`)**: Blank by default (email blocks remain hidden until a real email address is configured; `.example` addresses are rejected)
- **Opening Hours (`weekdaysHours`, `sundayHours`)**: Blank by default until actual showroom hours are added

### Editing Business Details Without Changing Website Code
1. Click **Adjust Contact, WhatsApp & Address** on the Home or Contact Us page (or **Store Contact Settings** in the footer).
2. Update any field (Business Name, Tagline, Phone, WhatsApp, Email, Address, Opening Hours, or Map Query).
3. Click **Save Showroom Details** for immediate live updates, or click **Download JSON** and upload the downloaded `business-config.json` into your hosted `public/` (or root `dist/`) folder.

---

## 2. Replacing Product Images & Updating the Catalogue

All 7 departments and sample product entries live in **`src/data/catalogue.ts`**.

### To update or add products:
1. Open `src/data/catalogue.ts`.
2. Locate the `SAMPLE_PRODUCTS` array.
3. For each item:
   - Set a unique `id`
   - Update `name` to the actual product name
   - Update `brand` to the real brand / manufacturer name
   - Choose `categoryId` (`'mens-fashion'`, `'womens-fashion'`, `'watches'`, `'perfumes'`, `'accessories'`, `'furniture'`, or `'electronics'`)
   - Match `subcategory` to one of the department's `subcategories`
   - Optionally add `price: '₹2,499'` (leave omitted if price should be shared on enquiry)
   - Update `description` and `specifications` (especially model numbers for Electronics, dimensions/materials for Furniture)
   - Set `isSample: false`

### To replace product images:
1. Place real product photos (`.jpg` or `.webp`, ideally `4:3` ratio, compressed under 300 KB) inside `public/products/` (e.g., `public/products/sofa-model-a.jpg`) or `src/assets/images/`.
2. Reference them in `src/data/catalogue.ts` (e.g. `image: '/products/sofa-model-a.jpg'`).
3. The brand logo is stored at `public/assets/aistudio/Screenshot_2026_1113_115602_2a6be01e.png` and referenced in `src/data/media.ts`.

---

## 3. Deployment Instructions (Free Hosting + Custom Domain)

This project builds into static files (`npm run build` → `dist/`) and requires **no paid servers or databases**.

### Option A: GitHub Pages (Free, Automated via GitHub Actions)
1. Create a new GitHub repository and push all project files (including `.github/workflows/deploy.yml`, `public/`, and `src/`).
2. In your GitHub repository, go to **Settings → Pages**.
3. Under **Build and deployment → Source**, select **GitHub Actions**.
4. Every push to the `main` branch automatically runs type-checking, unit tests, builds `dist/` with the repository base path, copies `index.html` to `404.html` for SPA routing, and deploys live.
5. **Custom Domain**: Add your domain in **Settings → Pages → Custom domain** and add a `public/CNAME` file containing your domain name (the workflow automatically switches `VITE_BASE_PATH` to `/`).

### Option B: Vercel (Free Tier)
1. Push this repository to a GitHub account owned by the client.
2. Log in at [vercel.com](https://vercel.com) with GitHub and click **Add New → Project**.
3. Select the repository. Vercel auto-detects Vite (`Build Command: npm run build`, `Output Directory: dist`). `vercel.json` is already included for clean routing across all 10 pages.
4. Click **Deploy**.
5. **Custom Domain**: Open **Project Settings → Domains**, enter your purchased domain (e.g., `sachinjeansfurniture.com`), and add the DNS `A` / `CNAME` records shown by Vercel at your domain registrar.

### Option C: Netlify (Free Tier)
1. Connect the GitHub repository on [netlify.com](https://app.netlify.com).
2. Build command: `npm run build` | Publish directory: `dist` (`public/_redirects` is already included for SPA routing).
3. Add your custom domain under **Domain Management** and enable free automatic HTTPS.

### Option D: Cloudflare Pages (Free Tier)
1. Connect the GitHub repository in Cloudflare Dashboard → **Workers & Pages**.
2. Build command: `npm run build` | Build output directory: `dist`.

---

## 4. SEO Basics Implemented

- Semantic HTML5 landmarks (`<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<footer>`).
- Dynamic `<title>` and `<meta name="description">` updates when navigating across all 10 pages.
- OpenGraph (`og:title`, `og:description`, `og:type`) and Twitter Card tags in `index.html`.
- Schema.org `DepartmentStore` JSON-LD structured data in `index.html` (update the JSON-LD phone and address in `index.html` when publishing real store details).
- Descriptive `alt` attributes on all images.

---

## 5. Testing Checklist

- [ ] Verify all 10 pages load cleanly (`/`, `/about`, `/mens-fashion`, `/womens-fashion`, `/watches`, `/perfumes`, `/accessories`, `/furniture`, `/electronics`, `/contact`).
- [ ] Test subcategory filter buttons and search input on category pages.
- [ ] Click **Enquire on WhatsApp** on a product card and verify the pre-filled message reads:
  `Hello, I am interested in [Product Name] at Sachin Jeans & Furniture. Please share the price and availability.`
- [ ] Test **Adjust Contact, WhatsApp & Address** on `/contact` and confirm phone, WhatsApp links, address, and map update immediately.
- [ ] Check mobile menu drawer and layout at `390px` mobile width, tablet, and `1440px` desktop width with zero horizontal overflow.
- [ ] Run `npm run lint` and `npm run build` cleanly before deploying.
- [ ] /* /index.html 200
- [ ] {
  "businessName": "Sachin Jeans & Furniture",
  "tagline": "Fashion · Comfort · Better Living",
  "phoneDisplay": "+91 62680 57508",
  "whatsappNumber": "916268057508",
  "email": "",
  "addressLine1": "Gol Bazar, Devarhat",
  "addressLine2": "गोल बाजार, देवरहट",
  "cityStatePostal": "",
  "mapQuery": "Gol Bazar, Devarhat",
  "weekdaysHours": "",
  "sundayHours": ""
}
import {createRoot} from 'react-dom/client';
import App from './App.tsx';
import './index.css';

createRoot(document.getElementById('root')!).render(<App />);
@import "tailwindcss";

@theme {
  --font-display: "Playfair Display", Georgia, serif;
  --font-sans: "Plus Jakarta Sans", -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
  --color-canvas: #FAF8F5;
  --color-surface: #F2EDE4;
  --color-surface-elevated: #FFFFFF;
  --color-charcoal: #1B1917;
  --color-charcoal-muted: #5A544E;
  --color-border-warm: #DFD6C7;
  --color-gold: #A68142;
  --color-gold-light: #D4AF6A;
}

@layer base {
  html {
    font-family: var(--font-sans);
    scroll-behavior: smooth;
    background-color: #FAF8F5;
    color: #1B1917;
  }

  h1, h2, h3, .font-display {
    font-family: var(--font-display);
  }
}

.text-balance {
  text-wrap: balance;
}

@media (prefers-reduced-motion: reduce) {
  html {
    scroll-behavior: auto;
  }
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}
import { useState, useEffect, useCallback } from 'react';
import {
  DEFAULT_BUSINESS_CONFIG,
  STORE_CONFIG_STORAGE_KEY,
  mergeBusinessConfig,
  type BusinessConfig,
  type EditableBusinessFields,
} from './config/businessConfig';
import { CATEGORIES } from './data/catalogue';
import {
  buildRoutePath,
  getCategoryByRoute,
  stripBasePath,
  type PageRoute,
  type ProductItem,
} from './utils/catalogueLogic';
import { Header } from './components/Header';
import { Footer } from './components/Footer';
import { ProductModal } from './components/ProductModal';
import { StoreSettingsModal } from './components/StoreSettingsModal';
import { HomePage } from './pages/HomePage';
import { AboutPage } from './pages/AboutPage';
import { ContactPage } from './pages/ContactPage';
import { CategoryPage } from './pages/CategoryPage';

const BASE_URL = import.meta.env.BASE_URL || '/';

function readStoredOverrides(): Partial<EditableBusinessFields> | null {
  if (typeof window === 'undefined') return null;
  try {
    const raw = window.localStorage.getItem(STORE_CONFIG_STORAGE_KEY);
    return raw ? (JSON.parse(raw) as Partial<EditableBusinessFields>) : null;
  } catch {
    return null;
  }
}

function loadInitialBusinessConfig(): BusinessConfig {
  return mergeBusinessConfig(DEFAULT_BUSINESS_CONFIG, readStoredOverrides());
}

export default function App() {
  const [currentRoute, setCurrentRoute] = useState<PageRoute>(() =>
    typeof window !== 'undefined' ? stripBasePath(window.location.pathname, BASE_URL) : '/'
  );
  const [baseFileConfig, setBaseFileConfig] = useState<BusinessConfig>(DEFAULT_BUSINESS_CONFIG);
  const [config, setConfig] = useState<BusinessConfig>(loadInitialBusinessConfig);
  const [selectedProduct, setSelectedProduct] = useState<ProductItem | null>(null);
  const [settingsOpen, setSettingsOpen] = useState(false);

  // Load editable public/business-config.json without requiring code edits
  useEffect(() => {
    let active = true;
    fetch(`${BASE_URL}business-config.json`, { cache: 'no-store' })
      .then((res) => (res.ok ? res.json() : null))
      .then((json: Partial<EditableBusinessFields> | null) => {
        if (!active || !json) return;
        const mergedFileBase = mergeBusinessConfig(DEFAULT_BUSINESS_CONFIG, json);
        setBaseFileConfig(mergedFileBase);
        setConfig(mergeBusinessConfig(mergedFileBase, readStoredOverrides()));
      })
      .catch(() => {
        // Fallback silently to DEFAULT_BUSINESS_CONFIG if offline or unavailable
      });

    return () => {
      active = false;
    };
  }, []);

  const navigate = useCallback((route: PageRoute) => {
    setCurrentRoute(route);
    if (typeof window !== 'undefined') {
      const targetPath = buildRoutePath(route, BASE_URL);
      if (window.location.pathname !== targetPath) {
        window.history.pushState({}, '', targetPath);
      }
      window.scrollTo({ top: 0, behavior: 'smooth' });
    }
  }, []);

  useEffect(() => {
    const handlePopState = () => {
      setCurrentRoute(stripBasePath(window.location.pathname, BASE_URL));
    };
    window.addEventListener('popstate', handlePopState);
    return () => window.removeEventListener('popstate', handlePopState);
  }, []);

  // Update document title & description dynamically per route for SEO & browser tabs
  useEffect(() => {
    const category = getCategoryByRoute(CATEGORIES, currentRoute);
    let title = `${config.businessName} – Style, Comfort & Everything You Need`;
    let description =
      `Explore men's and women's fashion, watches, perfumes, accessories, furniture, and electronics under one roof at ${config.businessName}.`;

    if (category) {
      title = `${category.title} | ${config.businessName}`;
      description = category.description;
    } else if (currentRoute === '/about') {
      title = `About Us | ${config.businessName}`;
      description =
        `Learn about ${config.businessName} — a multi-category retail showroom offering established apparel, accessories, furniture, and electronics brands.`;
    } else if (currentRoute === '/contact') {
      title = `Contact Us | ${config.businessName}`;
      description =
        `Contact ${config.businessName} via WhatsApp or phone, view business hours, and find showroom directions on Google Maps.`;
    }

    document.title = title;
    const metaDesc = document.querySelector('meta[name="description"]');
    if (metaDesc) {
      metaDesc.setAttribute('content', description);
    }
  }, [currentRoute, config.businessName]);

  const handleSaveSettings = (fields: EditableBusinessFields) => {
    try {
      window.localStorage.setItem(STORE_CONFIG_STORAGE_KEY, JSON.stringify(fields));
    } catch {
      // Ignore storage quota restrictions
    }
    setConfig(mergeBusinessConfig(baseFileConfig, fields));
  };

  const handleResetSettings = () => {
    try {
      window.localStorage.removeItem(STORE_CONFIG_STORAGE_KEY);
    } catch {
      // Ignore storage errors
    }
    setConfig(baseFileConfig);
  };

  const activeCategory = getCategoryByRoute(CATEGORIES, currentRoute);

  return (
    <div className="min-h-screen flex flex-col bg-[#FAF8F5] text-[#1B1917]">
      <Header currentRoute={currentRoute} onNavigate={navigate} config={config} />

      <main className="flex-1">
        {currentRoute === '/' && (
          <HomePage
            config={config}
            onNavigate={navigate}
            onSelectProduct={setSelectedProduct}
            onOpenSettings={() => setSettingsOpen(true)}
          />
        )}

        {currentRoute === '/about' && (
          <AboutPage config={config} onNavigate={navigate} />
        )}

        {currentRoute === '/contact' && (
          <ContactPage config={config} onOpenSettings={() => setSettingsOpen(true)} />
        )}

        {activeCategory && (
          <CategoryPage
            category={activeCategory}
            config={config}
            onNavigate={navigate}
            onSelectProduct={setSelectedProduct}
          />
        )}
      </main>

      <Footer
        onNavigate={navigate}
        config={config}
        onOpenSettings={() => setSettingsOpen(true)}
      />

      <ProductModal
        product={selectedProduct}
        config={config}
        onClose={() => setSelectedProduct(null)}
      />

      <StoreSettingsModal
        isOpen={settingsOpen}
        config={config}
        onSave={handleSaveSettings}
        onReset={handleResetSettings}
        onClose={() => setSettingsOpen(false)}
      />
    </div>
  );
}
export interface BusinessConfig {
  businessName: string;
  tagline: string;
  phoneDisplay: string;
  phoneHref: string;
  whatsappNumber: string;
  email: string;
  addressLine1: string;
  addressLine2: string;
  cityStatePostal: string;
  mapQuery: string;
  businessHours: {
    weekdays: string;
    sunday: string;
  };
}

/**
 * CENTRAL BUSINESS CONFIGURATION
 * -------------------------------------------------------------------------
 * Single source of truth for Sachin Jeans & Furniture contact information.
 * Verified from shop signboard:
 *   - Phone & WhatsApp: 6268057508 (+91 62680 57508)
 *   - Address: Gol Bazar, Devarhat (गोल बाजार, देवरहट)
 *
 * To edit without modifying TypeScript code:
 *   1. Edit `public/business-config.json` directly, OR
 *   2. Click "Adjust Contact, WhatsApp & Address" on the website and use
 *      "Download business-config.json" to save and replace `public/business-config.json`.
 */
export const DEFAULT_BUSINESS_CONFIG: BusinessConfig = {
  businessName: 'Sachin Jeans & Furniture',
  tagline: 'Fashion · Comfort · Better Living',
  phoneDisplay: '+91 62680 57508',
  phoneHref: '+916268057508',
  whatsappNumber: '916268057508',
  email: '',
  addressLine1: 'Gol Bazar, Devarhat',
  addressLine2: 'गोल बाजार, देवरहट',
  cityStatePostal: '',
  mapQuery: 'Gol Bazar, Devarhat',
  businessHours: {
    weekdays: '',
    sunday: '',
  },
};

export const STORE_CONFIG_STORAGE_KEY = 'sjf_adjustable_store_config_v3';

export interface EditableBusinessFields {
  businessName: string;
  tagline: string;
  phoneDisplay: string;
  whatsappNumber: string;
  email: string;
  addressLine1: string;
  addressLine2: string;
  cityStatePostal: string;
  mapQuery: string;
  weekdaysHours: string;
  sundayHours: string;
}

export function sanitizeDialablePhone(raw: string): string {
  const cleaned = raw.replace(/[^\d+]/g, '');
  return cleaned || DEFAULT_BUSINESS_CONFIG.phoneHref;
}

export function hasConfiguredEmail(email?: string | null): boolean {
  if (!email) return false;
  const trimmed = email.trim().toLowerCase();
  if (!trimmed || !trimmed.includes('@') || !trimmed.includes('.')) {
    return false;
  }
  if (trimmed.endsWith('.example') || trimmed.includes('@example.')) {
    return false;
  }
  return true;
}

export function hasConfiguredHours(config: BusinessConfig): boolean {
  return Boolean(
    config.businessHours.weekdays.trim() || config.businessHours.sunday.trim()
  );
}

export function mergeBusinessConfig(
  base: BusinessConfig,
  overrides?: Partial<EditableBusinessFields> | null
): BusinessConfig {
  if (!overrides) return base;

  const businessName = overrides.businessName?.trim() || base.businessName;
  const tagline = overrides.tagline?.trim() || base.tagline;
  const phoneDisplay = overrides.phoneDisplay?.trim() || base.phoneDisplay;
  const whatsappNumber = overrides.whatsappNumber?.trim() || base.whatsappNumber;
  const addressLine1 = overrides.addressLine1?.trim() || base.addressLine1;
  const addressLine2 =
    overrides.addressLine2 !== undefined ? overrides.addressLine2.trim() : base.addressLine2;
  const cityStatePostal =
    overrides.cityStatePostal !== undefined
      ? overrides.cityStatePostal.trim()
      : base.cityStatePostal;
  const mapQuery =
    overrides.mapQuery?.trim() ||
    [addressLine1, cityStatePostal].filter(Boolean).join(', ') ||
    base.mapQuery;
  const rawEmail = overrides.email !== undefined ? overrides.email.trim() : base.email;
  const email = hasConfiguredEmail(rawEmail) ? rawEmail : '';
  const weekdays =
    overrides.weekdaysHours !== undefined
      ? overrides.weekdaysHours.trim()
      : base.businessHours.weekdays;
  const sunday =
    overrides.sundayHours !== undefined
      ? overrides.sundayHours.trim()
      : base.businessHours.sunday;

  return {
    ...base,
    businessName,
    tagline,
    phoneDisplay,
    phoneHref: sanitizeDialablePhone(phoneDisplay),
    whatsappNumber,
    email,
    addressLine1,
    addressLine2,
    cityStatePostal,
    mapQuery,
    businessHours: {
      weekdays,
      sunday,
    },
  };
}

export function toEditableBusinessFields(config: BusinessConfig): EditableBusinessFields {
  return {
    businessName: config.businessName,
    tagline: config.tagline,
    phoneDisplay: config.phoneDisplay,
    whatsappNumber: config.whatsappNumber,
    email: config.email,
    addressLine1: config.addressLine1,
    addressLine2: config.addressLine2,
    cityStatePostal: config.cityStatePostal,
    mapQuery: config.mapQuery,
    weekdaysHours: config.businessHours.weekdays,
    sundayHours: config.businessHours.sunday,
  };
}

export function formatFullAddress(config: BusinessConfig): string {
  return [config.addressLine1, config.addressLine2, config.cityStatePostal]
    .filter((part) => part && part.trim().length > 0)
    .join(', ');
}
import heroShowroomImg from '../assets/images/hero_showroom_interior_1794551335043.jpg';
import mensFashionImg from '../assets/images/cat_mens_fashion_1794551335253.jpg';
import womensFashionImg from '../assets/images/cat_womens_fashion_1794551335354.jpg';
import watchesImg from '../assets/images/cat_watches_1794551336180.jpg';
import perfumesImg from '../assets/images/cat_perfumes_1794551336001.jpg';
import accessoriesImg from '../assets/images/cat_accessories_1794551337004.jpg';
import furnitureImg from '../assets/images/cat_furniture_1794551336508.jpg';
import electronicsImg from '../assets/images/cat_electronics_1794551338094.jpg';

export const BRAND_LOGO_URL = `${import.meta.env.BASE_URL}assets/aistudio/Screenshot_2026_1113_115602_2a6be01e.png`;

export const SHOWROOM_MEDIA = {
  heroShowroom: heroShowroomImg,
  mensFashion: mensFashionImg,
  womensFashion: womensFashionImg,
  watches: watchesImg,
  perfumes: perfumesImg,
  accessories: accessoriesImg,
  furniture: furnitureImg,
  electronics: electronicsImg,
} as const;
import { SHOWROOM_MEDIA } from './media';
import type { CategoryMeta, ProductItem } from '../utils/catalogueLogic';

/**
 * PRODUCT CATEGORIES CONFIGURATION
 * -------------------------------------------------------------------------
 * All 7 core showroom departments and their navigable subcategories.
 */
export const CATEGORIES: CategoryMeta[] = [
  {
    id: 'mens-fashion',
    route: '/mens-fashion',
    title: "Men's Collection",
    shortTitle: "Men's Fashion",
    tagline: 'Denim, shirting, trousers & everyday wardrobe essentials',
    description:
      'Explore men’s apparel from multiple established clothing brands — including jeans, casual and formal shirts, T-shirts, trousers, and coordinated men’s accessories.',
    heroImage: SHOWROOM_MEDIA.mensFashion,
    subcategories: [
      'All',
      'Jeans',
      'Shirts',
      'T-Shirts',
      'Trousers',
      'Casual Wear',
      'Formal Wear',
      "Men's Accessories",
    ],
  },
  {
    id: 'womens-fashion',
    route: '/womens-fashion',
    title: "Women's Collection",
    shortTitle: "Women's Fashion",
    tagline: 'Ethnic silhouettes, western staples, tops & denim',
    description:
      'Discover women’s ethnic wear, western wear, tops, jeans, casual outfits, and seasonal multi-brand fashion collections curated for daily comfort and special occasions.',
    heroImage: SHOWROOM_MEDIA.womensFashion,
    subcategories: [
      'All',
      'Ethnic Wear',
      'Western Wear',
      'Tops',
      'Jeans',
      'Casual Wear',
      'Fashion Collections',
    ],
  },
  {
    id: 'watches',
    route: '/watches',
    title: 'Watches',
    shortTitle: 'Watches',
    tagline: 'Men’s and women’s timepieces across classic and modern styles',
    description:
      'Browse analog, dress, and everyday wristwatches from multiple watchmakers — available in stainless steel bracelets, leather straps, and contemporary dial finishes.',
    heroImage: SHOWROOM_MEDIA.watches,
    subcategories: [
      'All',
      "Men's Watches",
      "Women's Watches",
      'Classic & Dress Styles',
      'Everyday & Chronograph',
    ],
  },
  {
    id: 'perfumes',
    route: '/perfumes',
    title: 'Perfumes',
    shortTitle: 'Perfumes',
    tagline: 'Men’s & women’s fragrances across woody, floral & fresh notes',
    description:
      'Explore Eau de Parfum, Eau de Toilette, and everyday fragrance collections for men and women from established fragrance houses.',
    heroImage: SHOWROOM_MEDIA.perfumes,
    subcategories: [
      'All',
      "Men's Fragrances",
      "Women's Fragrances",
      'Fragrance Collections',
    ],
  },
  {
    id: 'accessories',
    route: '/accessories',
    title: 'Fashion Accessories',
    shortTitle: 'Accessories',
    tagline: 'Belts, wallets, eyewear & everyday finishing touches',
    description:
      'Complete your wardrobe with formal and casual leather belts, wallets, eyewear, and other practical fashion accessories stocked in our showroom.',
    heroImage: SHOWROOM_MEDIA.accessories,
    subcategories: ['All', 'Belts', 'Other Available Accessories'],
  },
  {
    id: 'furniture',
    route: '/furniture',
    title: 'Furniture',
    shortTitle: 'Furniture',
    tagline: 'Sofas, beds, wardrobes, tables & chairs for modern homes',
    description:
      'Furnish living rooms, bedrooms, and dining spaces with sofas, beds, wardrobes, tables, chairs, and home storage solutions sourced from trusted furniture manufacturers.',
    heroImage: SHOWROOM_MEDIA.furniture,
    subcategories: [
      'All',
      'Sofas',
      'Beds',
      'Wardrobes',
      'Tables',
      'Chairs',
      'Other Furniture Products',
    ],
  },
  {
    id: 'electronics',
    route: '/electronics',
    title: 'Electronics',
    shortTitle: 'Electronics',
    tagline: 'Home entertainment, appliances & everyday electronics',
    description:
      'Compare brand models and technical specifications on televisions, audio systems, home appliances, and everyday electronics available at our showroom.',
    heroImage: SHOWROOM_MEDIA.electronics,
    subcategories: [
      'All',
      'Televisions & Audio',
      'Home Appliances',
      'Smart & Personal Electronics',
    ],
  },
];

/**
 * SAMPLE PRODUCT CATALOGUE (DEMONSTRATION ENTRIES)
 * -------------------------------------------------------------------------
 * HOW TO ADD OR UPDATE PRODUCTS:
 * 1. Copy an existing object in the array below.
 * 2. Update `id`, `name`, `brand` (actual manufacturer/brand name), `categoryId`,
 *    `subcategory`, `description`, and optional `price` (e.g. '₹1,999').
 * 3. Replace `image` with your real product photograph path or imported asset.
 * 4. Set `isSample: false` once you replace demonstration entries with real stock.
 */
export const SAMPLE_PRODUCTS: ProductItem[] = [
  // --- A. MEN'S FASHION ---
  {
    id: 'mf-jeans-01',
    name: 'Sample Indigo Stretch Denim Jeans',
    brand: 'Established Denim Brand (Sample)',
    categoryId: 'mens-fashion',
    categoryLabel: "Men's Fashion",
    subcategory: 'Jeans',
    description:
      'Sample product entry representing classic indigo five-pocket denim jeans available in slim, tapered, and regular fits across stocked brands.',
    image: SHOWROOM_MEDIA.mensFashion,
    featured: true,
    isSample: true,
    specifications: [
      { label: 'Category', value: "Men's Jeans" },
      { label: 'Fits Available', value: 'Slim / Regular / Tapered (Sample)' },
      { label: 'Fabric', value: 'Cotton Stretch Denim (Sample)' },
    ],
  },
  {
    id: 'mf-shirt-01',
    name: 'Sample Textured Cotton Formal & Casual Shirt',
    brand: 'Multi-Brand Shirting (Sample)',
    categoryId: 'mens-fashion',
    categoryLabel: "Men's Fashion",
    subcategory: 'Shirts',
    description:
      'Sample entry for crisp button-down cotton and linen-blend shirts suited for office wear and weekend dressing.',
    image: SHOWROOM_MEDIA.mensFashion,
    isSample: true,
    specifications: [
      { label: 'Style', value: 'Full Sleeve / Button-Down (Sample)' },
      { label: 'Collar', value: 'Spread & Classic Collar Options' },
    ],
  },
  {
    id: 'mf-tshirt-01',
    name: 'Sample Crew Neck & Polo T-Shirt Range',
    brand: 'Apparel Brand Placeholder',
    categoryId: 'mens-fashion',
    categoryLabel: "Men's Fashion",
    subcategory: 'T-Shirts',
    description:
      'Sample demonstration item for combed cotton crew-neck tees and breathable knit polo shirts in seasonal solid shades.',
    image: SHOWROOM_MEDIA.mensFashion,
    isSample: true,
    specifications: [
      { label: 'Neckline', value: 'Crew Neck & Collar Polo (Sample)' },
      { label: 'Material', value: 'Combed Cotton Knit (Sample)' },
    ],
  },
  {
    id: 'mf-trousers-01',
    name: 'Sample Pleated & Chino Trousers',
    brand: 'Menswear Brand Placeholder',
    categoryId: 'mens-fashion',
    categoryLabel: "Men's Fashion",
    subcategory: 'Trousers',
    description:
      'Sample entry for tailored cotton chinos and formal pleated trousers in neutral charcoal, khaki, and stone tones.',
    image: SHOWROOM_MEDIA.mensFashion,
    isSample: true,
    specifications: [
      { label: 'Wear Type', value: 'Smart Casual & Office (Sample)' },
      { label: 'Waist Sizes', value: 'Check in-store size availability' },
    ],
  },
  {
    id: 'mf-casual-01',
    name: 'Sample Weekend Casual Wear Set',
    brand: 'Multi-Brand Selection (Sample)',
    categoryId: 'mens-fashion',
    categoryLabel: "Men's Fashion",
    subcategory: 'Casual Wear',
    description:
      'Sample casual wear pairing featuring relaxed overshirts, breathable tees, and everyday denim.',
    image: SHOWROOM_MEDIA.mensFashion,
    isSample: true,
  },
  {
    id: 'mf-formal-01',
    name: 'Sample Two-Piece Formal Wear Pairing',
    brand: 'Formalwear Brand Placeholder',
    categoryId: 'mens-fashion',
    categoryLabel: "Men's Fashion",
    subcategory: 'Formal Wear',
    description:
      'Sample formal menswear selection including structured shirts, tailored trousers, and matching blazers.',
    image: SHOWROOM_MEDIA.mensFashion,
    isSample: true,
  },
  {
    id: 'mf-acc-01',
    name: "Sample Men's Gift & Styling Accessories",
    brand: 'Accessories Brand Placeholder',
    categoryId: 'mens-fashion',
    categoryLabel: "Men's Fashion",
    subcategory: "Men's Accessories",
    description:
      'Sample entry covering pocket squares, ties, socks, and coordinated men’s wardrobe accessories stocked in-store.',
    image: SHOWROOM_MEDIA.accessories,
    isSample: true,
  },

  // --- B. WOMEN'S FASHION ---
  {
    id: 'wf-ethnic-01',
    name: 'Sample Embroidered Straight Kurta Set',
    brand: 'Ethnicwear Brand Placeholder',
    categoryId: 'womens-fashion',
    categoryLabel: "Women's Fashion",
    subcategory: 'Ethnic Wear',
    description:
      'Sample demonstration product for cotton-silk and breathable festive kurtas, dupattas, and ethnic sets.',
    image: SHOWROOM_MEDIA.womensFashion,
    featured: true,
    isSample: true,
    specifications: [
      { label: 'Category', value: "Women's Ethnic Wear" },
      { label: 'Work', value: 'Thread Embroidery (Sample)' },
    ],
  },
  {
    id: 'wf-western-01',
    name: 'Sample Tailored Linen Blend Western Wear',
    brand: 'Westernwear Brand Placeholder',
    categoryId: 'womens-fashion',
    categoryLabel: "Women's Fashion",
    subcategory: 'Western Wear',
    description:
      'Sample entry for structured western dresses, co-ord sets, and smart everyday silhouettes.',
    image: SHOWROOM_MEDIA.womensFashion,
    isSample: true,
  },
  {
    id: 'wf-tops-01',
    name: 'Sample Relaxed Woven Tunic & Tops',
    brand: 'Womenswear Brand Placeholder',
    categoryId: 'womens-fashion',
    categoryLabel: "Women's Fashion",
    subcategory: 'Tops',
    description:
      'Sample demonstration item for crisp everyday blouses, printed tops, and collared workwear shirts.',
    image: SHOWROOM_MEDIA.womensFashion,
    isSample: true,
  },
  {
    id: 'wf-jeans-01',
    name: 'Sample High-Rise Straight Women’s Jeans',
    brand: 'Denim Brand Placeholder',
    categoryId: 'womens-fashion',
    categoryLabel: "Women's Fashion",
    subcategory: 'Jeans',
    description:
      'Sample denim entry showcasing high-rise straight, wide-leg, and skinny-fit women’s jeans.',
    image: SHOWROOM_MEDIA.womensFashion,
    isSample: true,
  },
  {
    id: 'wf-casual-01',
    name: 'Sample Everyday Casual Lounge & Daywear',
    brand: 'Multi-Brand Selection (Sample)',
    categoryId: 'womens-fashion',
    categoryLabel: "Women's Fashion",
    subcategory: 'Casual Wear',
    description:
      'Sample casual wear range designed for breathable all-day comfort across seasons.',
    image: SHOWROOM_MEDIA.womensFashion,
    isSample: true,
  },
  {
    id: 'wf-collection-01',
    name: 'Sample Seasonal Fashion Collection Showcase',
    brand: 'Curated Multi-Brand (Sample)',
    categoryId: 'womens-fashion',
    categoryLabel: "Women's Fashion",
    subcategory: 'Fashion Collections',
    description:
      'Sample seasonal collection highlight featuring coordinated ethnic and contemporary western arrivals.',
    image: SHOWROOM_MEDIA.womensFashion,
    isSample: true,
  },

  // --- C. WATCHES ---
  {
    id: 'wt-men-01',
    name: 'Sample Classic Brushed Steel Dress Watch',
    brand: 'Watchmaker Brand Placeholder',
    categoryId: 'watches',
    categoryLabel: 'Watches',
    subcategory: "Men's Watches",
    description:
      'Sample men’s timepiece entry representing stainless-steel bracelet watches and formal leather-strap models.',
    image: SHOWROOM_MEDIA.watches,
    featured: true,
    isSample: true,
    specifications: [
      { label: 'Movement', value: 'Quartz / Automatic (Sample)' },
      { label: 'Case Material', value: 'Stainless Steel (Sample)' },
      { label: 'Strap Options', value: 'Metal Bracelet / Leather' },
    ],
  },
  {
    id: 'wt-women-01',
    name: 'Sample Champagne Dial Women’s Wristwatch',
    brand: 'Watchmaker Brand Placeholder',
    categoryId: 'watches',
    categoryLabel: 'Watches',
    subcategory: "Women's Watches",
    description:
      'Sample women’s wristwatch entry featuring slim-profile cases, champagne or mother-of-pearl dials, and delicate straps.',
    image: SHOWROOM_MEDIA.watches,
    isSample: true,
    specifications: [
      { label: 'Dial Style', value: 'Minimalist Analog (Sample)' },
      { label: 'Strap', value: 'Leather / Mesh Bracelet (Sample)' },
    ],
  },
  {
    id: 'wt-style-01',
    name: 'Sample Multi-Dial Chronograph & Casual Watch',
    brand: 'Watch Brand Placeholder',
    categoryId: 'watches',
    categoryLabel: 'Watches',
    subcategory: 'Everyday & Chronograph',
    description:
      'Sample entry representing sporty chronographs and versatile everyday timepieces stocked across brands.',
    image: SHOWROOM_MEDIA.watches,
    isSample: true,
    specifications: [
      { label: 'Water Resistance', value: 'Model-dependent (Enquire in-store)' },
      { label: 'Display', value: 'Analog Multi-Dial (Sample)' },
    ],
  },
  {
    id: 'wt-classic-01',
    name: 'Sample Heritage Leather Strap Timepiece',
    brand: 'Watch Brand Placeholder',
    categoryId: 'watches',
    categoryLabel: 'Watches',
    subcategory: 'Classic & Dress Styles',
    description:
      'Sample dress timepiece designed for formal occasions and gifting.',
    image: SHOWROOM_MEDIA.watches,
    isSample: true,
  },

  // --- D. PERFUMES ---
  {
    id: 'pf-men-01',
    name: "Sample Woody & Amber Men's Eau de Parfum",
    brand: 'Fragrance House Placeholder',
    categoryId: 'perfumes',
    categoryLabel: 'Perfumes',
    subcategory: "Men's Fragrances",
    description:
      'Sample fragrance entry representing aromatic, woody, and warm spice compositions for men.',
    image: SHOWROOM_MEDIA.perfumes,
    featured: true,
    isSample: true,
    specifications: [
      { label: 'Concentration', value: 'Eau de Parfum / EDT (Sample)' },
      { label: 'Bottle Sizes', value: '50ml / 100ml Options (Sample)' },
    ],
  },
  {
    id: 'pf-women-01',
    name: "Sample Floral & Musk Women's Fragrance",
    brand: 'Fragrance House Placeholder',
    categoryId: 'perfumes',
    categoryLabel: 'Perfumes',
    subcategory: "Women's Fragrances",
    description:
      'Sample women’s perfume entry highlighting fresh floral, citrus, and soft musk fragrance profiles.',
    image: SHOWROOM_MEDIA.perfumes,
    isSample: true,
    specifications: [
      { label: 'Notes Profile', value: 'Floral & Soft Amber (Sample)' },
      { label: 'Packaging', value: 'Sealed Retail Box' },
    ],
  },
  {
    id: 'pf-coll-01',
    name: 'Sample Signature Gift & Discovery Fragrance Set',
    brand: 'Multi-Brand Fragrance (Sample)',
    categoryId: 'perfumes',
    categoryLabel: 'Perfumes',
    subcategory: 'Fragrance Collections',
    description:
      'Sample multi-bottle gift sets and unisex fragrance collections available for in-store testing.',
    image: SHOWROOM_MEDIA.perfumes,
    isSample: true,
  },

  // --- E. FASHION ACCESSORIES ---
  {
    id: 'ac-belt-01',
    name: 'Sample Reversible Full-Grain Leather Belt',
    brand: 'Leathercraft Brand Placeholder',
    categoryId: 'accessories',
    categoryLabel: 'Fashion Accessories',
    subcategory: 'Belts',
    description:
      'Sample belt entry representing formal black/brown reversible leather belts and casual brass-buckle styles.',
    image: SHOWROOM_MEDIA.accessories,
    featured: true,
    isSample: true,
    specifications: [
      { label: 'Material', value: 'Leather / Brass Buckle (Sample)' },
      { label: 'Sizes', value: 'Standard Waist Sizes Available' },
    ],
  },
  {
    id: 'ac-other-01',
    name: 'Sample Leather Wallet & Classic Eyewear',
    brand: 'Accessories Brand Placeholder',
    categoryId: 'accessories',
    categoryLabel: 'Fashion Accessories',
    subcategory: 'Other Available Accessories',
    description:
      'Sample retail item for bi-fold leather wallets, cardholders, sunglasses, and everyday carry accessories.',
    image: SHOWROOM_MEDIA.accessories,
    isSample: true,
    specifications: [
      { label: 'Items Included', value: 'Wallets, Cardholders, Sunglasses' },
    ],
  },

  // --- F. FURNITURE ---
  {
    id: 'fn-sofa-01',
    name: 'Sample Upholstered Three-Seater Living Sofa',
    brand: 'Furniture Manufacturer (Sample)',
    categoryId: 'furniture',
    categoryLabel: 'Furniture',
    subcategory: 'Sofas',
    description:
      'Sample living room sofa entry representing fabric, leatherette, and L-shaped sectional sofas available in our furniture gallery.',
    image: SHOWROOM_MEDIA.furniture,
    featured: true,
    isSample: true,
    specifications: [
      { label: 'Seating Type', value: '3-Seater / Sectional Options (Sample)' },
      { label: 'Upholstery', value: 'Woven Neutral Fabric (Sample)' },
      { label: 'Frame', value: 'Solid Wood Structure (Sample)' },
    ],
  },
  {
    id: 'fn-bed-01',
    name: 'Sample Storage Queen & King Platform Bed',
    brand: 'Furniture Manufacturer (Sample)',
    categoryId: 'furniture',
    categoryLabel: 'Furniture',
    subcategory: 'Beds',
    description:
      'Sample bedroom furniture entry covering upholstered and wooden queen/king beds with hydraulic or box storage options.',
    image: SHOWROOM_MEDIA.furniture,
    isSample: true,
    specifications: [
      { label: 'Sizes', value: 'Queen & King Options (Sample)' },
      { label: 'Storage', value: 'Box / Hydraulic Variants (Sample)' },
    ],
  },
  {
    id: 'fn-wardrobe-01',
    name: 'Sample Multi-Door Engineered & Solid Wood Wardrobe',
    brand: 'Furniture Manufacturer (Sample)',
    categoryId: 'furniture',
    categoryLabel: 'Furniture',
    subcategory: 'Wardrobes',
    description:
      'Sample wardrobe entry representing 2-door, 3-door, and sliding wardrobe configurations with hanging and shelf compartments.',
    image: SHOWROOM_MEDIA.furniture,
    isSample: true,
    specifications: [
      { label: 'Doors', value: '2-Door / 3-Door / Sliding (Sample)' },
      { label: 'Finish', value: 'Walnut & Matte Laminates (Sample)' },
    ],
  },
  {
    id: 'fn-table-01',
    name: 'Sample Solid Wood Coffee & Dining Table',
    brand: 'Furniture Manufacturer (Sample)',
    categoryId: 'furniture',
    categoryLabel: 'Furniture',
    subcategory: 'Tables',
    description:
      'Sample table entry covering center coffee tables, 4-to-6 seater dining tables, and compact study desks.',
    image: SHOWROOM_MEDIA.furniture,
    isSample: true,
  },
  {
    id: 'fn-chair-01',
    name: 'Sample Sculptural Accent & Dining Chair',
    brand: 'Furniture Manufacturer (Sample)',
    categoryId: 'furniture',
    categoryLabel: 'Furniture',
    subcategory: 'Chairs',
    description:
      'Sample seating entry showcasing lounge armchairs, upholstered dining chairs, and ergonomic home-office seating.',
    image: SHOWROOM_MEDIA.furniture,
    isSample: true,
  },
  {
    id: 'fn-other-01',
    name: 'Sample Media Console & Sideboard Unit',
    brand: 'Furniture Manufacturer (Sample)',
    categoryId: 'furniture',
    categoryLabel: 'Furniture',
    subcategory: 'Other Furniture Products',
    description:
      'Sample entry for TV media units, shoe racks, bookshelves, and bedside tables stocked in the showroom.',
    image: SHOWROOM_MEDIA.furniture,
    isSample: true,
  },

  // --- G. ELECTRONICS ---
  {
    id: 'el-tv-01',
    name: 'Sample 4K Smart LED Television & Soundbar',
    brand: 'Electronics Brand & Model Placeholder',
    categoryId: 'electronics',
    categoryLabel: 'Electronics',
    subcategory: 'Televisions & Audio',
    description:
      'Sample home entertainment product card demonstrating brand, model reference, and key technical specifications.',
    image: SHOWROOM_MEDIA.electronics,
    featured: true,
    isSample: true,
    specifications: [
      { label: 'Brand / Model', value: 'Specify Brand & Model Code Here' },
      { label: 
      /**
 * Pure WhatsApp & Google Maps URL builder utilities.
 */

export function sanitizePhoneForWhatsApp(rawPhone: string): string {
  const digits = rawPhone.replace(/\D/g, '');
  return digits || '916268057508';
}

export function buildProductEnquiryMessage(
  productName: string,
  businessName = 'Sachin Jeans & Furniture'
): string {
  const safeName = productName.trim() || 'your showroom product';
  return `Hello, I am interested in ${safeName} at ${businessName}. Please share the price and availability.`;
}

export function buildWhatsAppProductUrl(
  whatsappNumber: string,
  productName: string,
  businessName = 'Sachin Jeans & Furniture'
): string {
  const phone = sanitizePhoneForWhatsApp(whatsappNumber);
  const message = buildProductEnquiryMessage(productName, businessName);
  return `https://wa.me/${phone}?text=${encodeURIComponent(message)}`;
}

export function buildWhatsAppGeneralUrl(
  whatsappNumber: string,
  businessName = 'Sachin Jeans & Furniture',
  customMessage?: string
): string {
  const phone = sanitizePhoneForWhatsApp(whatsappNumber);
  const message =
    customMessage?.trim() ||
    `Hello, I would like to enquire about products and availability at ${businessName}.`;
  return `https://wa.me/${phone}?text=${encodeURIComponent(message)}`;
}

export function buildGoogleMapsUrl(query: string): string {
  const clean = query.trim() || 'Gol Bazar, Devarhat';
  return `https://www.google.com/maps/search/?api=1&query=${encodeURIComponent(clean)}`;
}

export function buildGoogleMapsEmbedUrl(query: string): string {
  const clean = query.trim() || 'Gol Bazar, Devarhat';
  return `https://maps.google.com/maps?q=${encodeURIComponent(clean)}&t=&z=15&ie=UTF8&iwloc=&output=embed`;
}
export type CategoryId =
  | 'mens-fashion'
  | 'womens-fashion'
  | 'watches'
  | 'perfumes'
  | 'accessories'
  | 'furniture'
  | 'electronics';

export type PageRoute =
  | '/'
  | '/about'
  | '/mens-fashion'
  | '/womens-fashion'
  | '/watches'
  | '/perfumes'
  | '/accessories'
  | '/furniture'
  | '/electronics'
  | '/contact';

export type ProductSortOption = 'featured' | 'name-asc' | 'name-desc';

export interface ProductSpec {
  label: string;
  value: string;
}

export interface ProductItem {
  id: string;
  name: string;
  brand: string;
  categoryId: CategoryId;
  categoryLabel: string;
  subcategory: string;
  price?: string;
  description: string;
  image: string;
  featured?: boolean;
  isSample?: boolean;
  specifications?: ProductSpec[];
}

export interface CategoryMeta {
  id: CategoryId;
  route: PageRoute;
  title: string;
  shortTitle: string;
  tagline: string;
  description: string;
  heroImage: string;
  subcategories: string[];
}

export const ALL_VALID_ROUTES: PageRoute[] = [
  '/',
  '/about',
  '/mens-fashion',
  '/womens-fashion',
  '/watches',
  '/perfumes',
  '/accessories',
  '/furniture',
  '/electronics',
  '/contact',
];

export function normalizePathname(pathname: string): PageRoute {
  const cleaned = pathname.replace(/\/+$/, '') || '/';
  if (ALL_VALID_ROUTES.includes(cleaned as PageRoute)) {
    return cleaned as PageRoute;
  }
  return '/';
}

export function stripBasePath(pathname: string, baseUrl = '/'): PageRoute {
  const normalizedBase = baseUrl.replace(/\/+$/, '');
  if (!normalizedBase || normalizedBase === '/') {
    return normalizePathname(pathname);
  }
  if (pathname === normalizedBase || pathname === `${normalizedBase}/`) {
    return '/';
  }
  if (pathname.startsWith(`${normalizedBase}/`)) {
    return normalizePathname(pathname.slice(normalizedBase.length));
  }
  return normalizePathname(pathname);
}

export function buildRoutePath(route: PageRoute, baseUrl = '/'): string {
  const normalizedBase = baseUrl.replace(/\/+$/, '');
  if (!normalizedBase || normalizedBase === '/') {
    return route;
  }
  return route === '/' ? `${normalizedBase}/` : `${normalizedBase}${route}`;
}

export interface FilterCriteria {
  categoryId?: CategoryId;
  subcategory?: string;
  searchQuery?: string;
  sortBy?: ProductSortOption;
  hideDemoItems?: boolean;
}

export function filterProducts(
  products: ProductItem[],
  criteria: FilterCriteria
): ProductItem[] {
  const { categoryId, subcategory, searchQuery, sortBy = 'featured', hideDemoItems = false } =
    criteria;
  const query = (searchQuery || '').trim().toLowerCase();

  const filtered = products.filter((item) => {
    if (hideDemoItems && item.isSample) {
      return false;
    }
    if (categoryId && item.categoryId !== categoryId) {
      return false;
    }
    if (subcategory && subcategory !== 'All' && item.subcategory !== subcategory) {
      return false;
    }
    if (query) {
      const searchable = [
        item.name,
        item.brand,
        item.categoryLabel,
        item.subcategory,
        item.description,
        ...(item.specifications || []).map((s) => `${s.label} ${s.value}`),
      ]
        .join(' ')
        .toLowerCase();
      if (!searchable.includes(query)) {
        return false;
      }
    }
    return true;
  });

  if (sortBy === 'name-asc') {
    return [...filtered].sort((a, b) => a.name.localeCompare(b.name));
  }
  if (sortBy === 'name-desc') {
    return [...filtered].sort((a, b) => b.name.localeCompare(a.name));
  }
  return [...filtered].sort((a, b) => Number(Boolean(b.featured)) - Number(Boolean(a.featured)));
}

export function getFeaturedProducts(products: ProductItem[], limit = 8): ProductItem[] {
  const featured = products.filter((p) => p.featured);
  return featured.slice(0, limit);
}

export function getCategoryByRoute(
  categories: CategoryMeta[],
  route: PageRoute
): CategoryMeta | undefined {
  return categories.find((c) => c.route === route);
}

export interface EnquiryFormInput {
  customerName: string;
  department: string;
  message: string;
}

export function validateEnquiryForm(input: EnquiryFormInput): string | null {
  if (!input.customerName.trim()) {
    return 'Please enter your name so our showroom team knows who to address.';
  }
  if (input.message.trim().length < 5) {
    return 'Please enter a brief enquiry message (at least 5 characters) about the item or category.';
  }
  return null;
}

export interface StoreSettingsValidationInput {
  businessName: string;
  phoneDisplay: string;
  whatsappNumber: string;
  email: string;
  addressLine1: string;
}

export function validateStoreSettings(input: StoreSettingsValidationInput): string | null {
  if (!input.businessName.trim()) {
    return 'Please enter the business name.';
  }
  if (!input.phoneDisplay.trim()) {
    return 'Please enter a contact phone number.';
  }
  const cleanWa = input.whatsappNumber.replace(/\D/g, '');
  if (cleanWa.length < 10) {
    return 'Please enter a valid WhatsApp number including country code (e.g. 916268057508).';
  }
  const trimmedEmail = input.email.trim().toLowerCase();
  if (trimmedEmail) {
    if (trimmedEmail.endsWith('.example') || trimmedEmail.includes('@example.')) {
      return 'Placeholder .example email addresses are not allowed. Leave blank or enter a real email.';
    }
    if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(trimmedEmail)) {
      return 'Please enter a valid email address or leave the email field empty.';
    }
  }
  if (!input.addressLine1.trim()) {
    return 'Please provide the showroom address.';
  }
  return null;
}
import test from 'node:test';
import assert from 'node:assert/strict';
import {
  DEFAULT_BUSINESS_CONFIG,
  formatFullAddress,
  hasConfiguredEmail,
  hasConfiguredHours,
  mergeBusinessConfig,
} from '../config/businessConfig';
import {
  buildGoogleMapsUrl,
  buildProductEnquiryMessage,
  buildWhatsAppGeneralUrl,
  buildWhatsAppProductUrl,
  sanitizePhoneForWhatsApp,
} from './whatsapp';
import {
  buildRoutePath,
  filterProducts,
  getFeaturedProducts,
  normalizePathname,
  stripBasePath,
  validateEnquiryForm,
  validateStoreSettings,
  type ProductItem,
} from './catalogueLogic';

const MOCK_PRODUCTS: ProductItem[] = [
  {
    id: 'p1',
    name: 'Zeta Denim Jeans',
    brand: 'Multi-Brand Selection (Sample)',
    categoryId: 'mens-fashion',
    categoryLabel: "Men's Fashion",
    subcategory: 'Jeans',
    description: 'Sample straight-cut indigo denim demonstration entry.',
    image: '/sample.jpg',
    featured: true,
    isSample: true,
  },
  {
    id: 'p2',
    name: 'Alpha Three-Seater Fabric Sofa',
    brand: 'Furniture Brand (Sample)',
    categoryId: 'furniture',
    categoryLabel: 'Furniture',
    subcategory: 'Sofas',
    price: '₹28,500',
    description: 'Live furniture entry.',
    image: '/sample-sofa.jpg',
    featured: false,
    isSample: false,
    specifications: [{ label: 'Seating Capacity', value: '3 Seater' }],
  },
  {
    id: 'p3',
    name: 'Beta Smart LED Television',
    brand: 'Electronics Brand (Sample)',
    categoryId: 'electronics',
    categoryLabel: 'Electronics',
    subcategory: 'Televisions & Audio',
    description: 'Sample television demonstration entry.',
    image: '/sample-tv.jpg',
    featured: true,
    isSample: true,
    specifications: [
      { label: 'Model', value: 'Sample Model Code' },
      { label: 'Display', value: '4K UHD Panel (Sample)' },
    ],
  },
];

test('sanitizePhoneForWhatsApp strips non-digits and falls back to 916268057508', () => {
  assert.equal(sanitizePhoneForWhatsApp('+91 62680-57508'), '916268057508');
  assert.equal(sanitizePhoneForWhatsApp(''), '916268057508');
});

test('hasConfiguredEmail rejects empty, invalid, and .example placeholders', () => {
  assert.equal(hasConfiguredEmail(''), false);
  assert.equal(hasConfiguredEmail('contact@sachinjeansfurniture.example'), false);
  assert.equal(hasConfiguredEmail('not-an-email'), false);
  assert.equal(hasConfiguredEmail('sales@sachinshowroom.in'), true);
});

test('hasConfiguredHours returns false when empty and true when set', () => {
  assert.equal(hasConfiguredHours(DEFAULT_BUSINESS_CONFIG), false);
  const withHours = mergeBusinessConfig(DEFAULT_BUSINESS_CONFIG, {
    weekdaysHours: 'Mon-Sat: 10 AM - 8 PM',
  });
  assert.equal(hasConfiguredHours(withHours), true);
});

test('buildProductEnquiryMessage generates exact requested WhatsApp template', () => {
  const msg = buildProductEnquiryMessage('Zeta Denim Jeans');
  assert.equal(
    msg,
    'Hello, I am interested in Zeta Denim Jeans at Sachin Jeans & Furniture. Please share the price and availability.'
  );
});

test('buildWhatsAppProductUrl and buildWhatsAppGeneralUrl use configured WhatsApp number', () => {
  const productUrl = buildWhatsAppProductUrl('916268057508', 'Beta Smart LED Television');
  assert.ok(productUrl.startsWith('https://wa.me/916268057508?text='));
  assert.ok(
    productUrl.includes(
      encodeURIComponent(
        'Hello, I am interested in Beta Smart LED Television at Sachin Jeans & Furniture. Please share the price and availability.'
      )
    )
  );

  const generalUrl = buildWhatsAppGeneralUrl('916268057508', 'Sachin Jeans & Furniture');
  assert.ok(generalUrl.startsWith('https://wa.me/916268057508?text='));
});

test('mergeBusinessConfig updates adjustable details and suppresses .example emails', () => {
  const merged = mergeBusinessConfig(DEFAULT_BUSINESS_CONFIG, {
    phoneDisplay: '+91 99887 76655',
    whatsappNumber: '919988776655',
    email: 'fake@domain.example',
    addressLine1: 'Shop 45, Station Road',
    addressLine2: 'Gol Bazar',
    cityStatePostal: 'Devarhat',
  });

  assert.equal(merged.phoneDisplay, '+91 99887 76655');
  assert.equal(merged.phoneHref, '+919988776655');
  assert.equal(merged.whatsappNumber, '919988776655');
  assert.equal(merged.email, '');
  assert.equal(
    formatFullAddress(merged),
    'Shop 45, Station Road, Gol Bazar, Devarhat'
  );
});

test('filterProducts supports category, subcategory, search, sortBy, and hideDemoItems', () => {
  assert.equal(filterProducts(MOCK_PRODUCTS, { categoryId: 'mens-fashion' }).length, 1);
  assert.equal(
    filterProducts(MOCK_PRODUCTS, { categoryId: 'furniture', subcategory: 'Sofas' }).length,
    1
  );
  assert.equal(filterProducts(MOCK_PRODUCTS, { searchQuery: '4K UHD' }).length, 1);
  assert.equal(filterProducts(MOCK_PRODUCTS, { hideDemoItems: true }).length, 1);

  const sortedAsc = filterProducts(MOCK_PRODUCTS, { sortBy: 'name-asc' });
  assert.equal(sortedAsc[0].id, 'p2');
  assert.equal(sortedAsc[2].id, 'p1');
});

test('validateEnquiryForm and validateStoreSettings catch invalid inputs', () => {
  assert.ok(
    validateEnquiryForm({ customerName: '', department: 'Watches', message: 'Check stock' })
  );
  assert.ok(
    validateEnquiryForm({ customerName: 'Amit', department: 'Watches', message: 'Hi' })
  );
  assert.equal(
    validateEnquiryForm({
      customerName: 'Amit',
      department: 'Watches',
      message: 'Please share availability of men watches.',
    }),
    null
  );

  assert.ok(
    validateStoreSettings({
      businessName: 'Sachin Jeans & Furniture',
      phoneDisplay: '+91 62680 57508',
      whatsappNumber: '916268057508',
      email: 'test@showroom.example',
      addressLine1: 'Gol Bazar, Devarhat',
    })
  );
  assert.equal(
    validateStoreSettings({
      businessName: 'Sachin Jeans & Furniture',
      phoneDisplay: '+91 62680 57508',
      whatsappNumber: '916268057508',
      email: '',
      addressLine1: 'Gol Bazar, Devarhat',
    }),
    null
  );
});

test('getFeaturedProducts returns only featured items up to limit', () => {
  const featured = getFeaturedProducts(MOCK_PRODUCTS, 4);
  assert.equal(featured.length, 2);
  assert.ok(featured.every((p) => p.featured));
});

test('normalizePathname resolves all 10 routes and falls back to /', () => {
  assert.equal(normalizePathname('/mens-fashion/'), '/mens-fashion');
  assert.equal(normalizePathname('/contact'), '/contact');
  assert.equal(normalizePathname('/unknown-route'), '/');
});

test('stripBasePath and buildRoutePath support GitHub Pages subpaths and root domains', () => {
  assert.equal(stripBasePath('/mens-fashion', '/'), '/mens-fashion');
  assert.equal(
    stripBasePath('/sachin-jeans-furniture/mens-fashion', '/sachin-jeans-furniture/'),
    '/mens-fashion'
  );
  assert.equal(
    stripBasePath('/sachin-jeans-furniture/', '/sachin-jeans-furniture/'),
    '/'
  );
  assert.equal(
    buildRoutePath('/furniture', '/sachin-jeans-furniture/'),
    '/sachin-jeans-furniture/furniture'
  );
  assert.equal(buildRoutePath('/', '/sachin-jeans-furniture/'), '/sachin-jeans-furniture/');
  assert.equal(buildRoutePath('/contact', '/'), '/contact');
});

test('buildGoogleMapsUrl builds encoded search URL', () => {
  const url = buildGoogleMapsUrl('Gol Bazar, Devarhat');
  assert.equal(
    url,
    'https://www.google.com/maps/search/?api=1&query=Gol%20Bazar%2C%20Devarhat'
  );
});
import { useState, useRef, useEffect } from 'react';
import { ChevronDown, Menu, X, MessageCircle } from 'lucide-react';
import { CATEGORIES } from '../data/catalogue';
import { BRAND_LOGO_URL } from '../data/media';
import type { PageRoute } from '../utils/catalogueLogic';
import type { BusinessConfig } from '../config/businessConfig';
import { buildWhatsAppGeneralUrl } from '../utils/whatsapp';

interface HeaderProps {
  currentRoute: PageRoute;
  onNavigate: (route: PageRoute) => void;
  config: BusinessConfig;
}

export function Header({ currentRoute, onNavigate, config }: HeaderProps) {
  const [collectionsOpen, setCollectionsOpen] = useState(false);
  const [mobileMenuOpen, setMobileMenuOpen] = useState(false);
  const headerRef = useRef<HTMLElement>(null);
  const dropdownRef = useRef<HTMLDivElement>(null);

  const isCategoryRoute = CATEGORIES.some((c) => c.route === currentRoute);

  // Close menus on route change
  useEffect(() => {
    setCollectionsOpen(false);
    setMobileMenuOpen(false);
  }, [currentRoute]);

  useEffect(() => {
    const handleClickOutside = (event: MouseEvent) => {
      const target = event.target as Node;
      if (dropdownRef.current && !dropdownRef.current.contains(target)) {
        setCollectionsOpen(false);
      }
      if (headerRef.current && !headerRef.current.contains(target)) {
        setMobileMenuOpen(false);
      }
    };
    const handleEscape = (event: KeyboardEvent) => {
      if (event.key === 'Escape') {
        setCollectionsOpen(false);
        setMobileMenuOpen(false);
      }
    };
    const handleResize = () => {
      if (window.innerWidth >= 1024) {
        setMobileMenuOpen(false);
      }
    };
    document.addEventListener('mousedown', handleClickOutside);
    document.addEventListener('keydown', handleEscape);
    window.addEventListener('resize', handleResize);
    return () => {
      document.removeEventListener('mousedown', handleClickOutside);
      document.removeEventListener('keydown', handleEscape);
      window.removeEventListener('resize', handleResize);
    };
  }, []);

  const handleLinkClick = (route: PageRoute) => {
    setCollectionsOpen(false);
    setMobileMenuOpen(false);
    onNavigate(route);
  };

  const whatsappUrl = buildWhatsAppGeneralUrl(config.whatsappNumber, config.businessName);

  return (
    <header
      ref={headerRef}
      className="sticky top-0 z-40 bg-[#FAF8F5]/95 backdrop-blur-md border-b border-[#DFD6C7]"
    >
      <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 md:h-20 flex items-center justify-between gap-8">
        {/* Zone 1: Single-line Brand Lockup */}
        <a
          href="/"
          onClick={(e) => {
            e.preventDefault();
            handleLinkClick('/');
          }}
          className="flex items-center gap-3 whitespace-nowrap shrink-0 focus-visible:outline-2 focus-visible:outline-offset-4 focus-visible:outline-[#A68142] rounded-sm"
        >
          <img
            src={BRAND_LOGO_URL}
            alt={`${config.businessName} Emblem`}
            referrerPolicy="no-referrer"
            className="w-9 h-9 md:w-10 md:h-10 rounded-full object-cover border border-[#C49B54]/60 shrink-0"
          />
          <span className="font-display text-lg md:text-xl font-semibold tracking-tight text-[#1B1917] whitespace-nowrap">
            {config.businessName}
          </span>
        </a>

        {/* Zone 2: Clean Single-Line Navigation Links */}
        <nav
          aria-label="Primary navigation"
          className="hidden lg:flex items-center gap-7 text-sm font-medium text-[#5A544E]"
        >
          <a
            href="/"
            onClick={(e) => {
              e.preventDefault();
              handleLinkClick('/');
            }}
            className={`whitespace-nowrap shrink-0 py-1 transition-colors hover:text-[#1B1917] ${
              currentRoute === '/'
                ? 'text-[#1B1917] border-b border-[#A68142]'
                : ''
            }`}
          >
            Home
          </a>

          <div ref={dropdownRef} className="relative">
            <button
              type="button"
              aria-expanded={collectionsOpen}
              aria-haspopup="true"
              onClick={() => setCollectionsOpen((prev) => !prev)}
              className={`inline-flex items-center gap-1.5 whitespace-nowrap shrink-0 py-1 transition-colors hover:text-[#1B1917] cursor-pointer ${
                isCategoryRoute
                  ? 'text-[#1B1917] border-b border-[#A68142]'
                  : ''
              }`}
            >
              <span>Collections</span>
              <ChevronDown
                className={`w-4 h-4 transition-transform duration-150 ${
                  collectionsOpen ? 'rotate-180' : ''
                }`}
                aria-hidden="true"
              />
            </button>

            {collectionsOpen && (
              <div
                role="menu"
                aria-label="Showroom collections"
                className="absolute left-0 top-full mt-3 w-64 bg-white border border-[#DFD6C7] rounded-lg shadow-lg py-2 z-50"
              >
                {CATEGORIES.map((category) => (
                  <a
                    key={category.id}
                    href={category.route}
                    role="menuitem"
                    onClick={(e) => {
                      e.preventDefault();
                      handleLinkClick(category.route);
                    }}
                    className={`block px-4 py-2.5 text-sm transition-colors ${
                      currentRoute === category.route
                        ? 'bg-[#F2EDE4] text-[#1B1917] font-semibold'
                        : 'text-[#5A544E] hover:bg-[#FAF8F5] hover:text-[#1B1917]'
                    }`}
                  >
                    {category.title}
                  </a>
                ))}
              </div>
            )}
          </div>

          <a
            href="/about"
            onClick={(e) => {
              e.preventDefault();
              handleLinkClick('/about');
            }}
            className={`whitespace-nowrap shrink-0 py-1 transition-colors hover:text-[#1B1917] ${
              currentRoute === '/about'
                ? 'text-[#1B1917] border-b border-[#A68142]'
                : ''
            }`}
          >
            About Us
          </a>

          <a
            href="/contact"
            onClick={(e) => {
              e.preventDefault();
              handleLinkClick('/contact');
            }}
            className={`whitespace-nowrap shrink-0 py-1 transition-colors hover:text-[#1B1917] ${
              currentRoute === '/contact'
                ? 'text-[#1B1917] border-b border-[#A68142]'
                : ''
            }`}
          >
            Contact Us
          </a>
        </nav>

        {/* Zone 3: Single Primary Action + Mobile Drawer Toggle */}
        <div className="flex items-center gap-3 shrink-0">
          <a
            href={whatsappUrl}
            target="_blank"
            rel="noopener noreferrer"
            className="hidden sm:inline-flex items-center gap-2 px-4 py-2.5 text-xs font-semibold tracking-wide bg-[#1B1917] text-[#FAF8F5] rounded-md hover:bg-[#322E2A] transition-colors whitespace-nowrap shrink-0 focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-[#A68142]"
          >
            <MessageCircle className="w-3.5 h-3.5 text-[#D4AF6A]" aria-hidden="true" />
            <span>WhatsApp Enquiry</span>
          </a>

          <button
            type="button"
            aria-label={mobileMenuOpen ? 'Close navigation menu' : 'Open navigation menu'}
            aria-expanded={mobileMenuOpen}
            aria-controls="mobile-nav-drawer"
            onClick={() => setMobileMenuOpen((prev) => !prev)}
            className="lg:hidden inline-flex items-center justify-center w-11 h-11 rounded-md border border-[#DFD6C7] text-[#1B1917] hover:bg-[#F2EDE4] transition-colors cursor-pointer"
          >
            {mobileMenuOpen ? (
              <X className="w-5 h-5" aria-hidden="true" />
            ) : (
              <Menu className="w-5 h-5" aria-hidden="true" />
            )}
          </button>
        </div>
      </div>

      {/* Mobile Navigation Drawer */}
      {mobileMenuOpen && (
        <nav
          id="mobile-nav-drawer"
          aria-label="Mobile navigation"
          className="lg:hidden border-t border-[#DFD6C7] bg-[#FAF8F5] px-4 py-5 max-h-[80vh] overflow-y-auto shadow-lg"
        >
          <div className="space-y-1">
            <a
              href="/"
              onClick={(e) => {
                e.preventDefault();
                handleLinkClick('/');
              }}
              className={`block px-3 py-2.5 rounded-md text-sm font-medium ${
                currentRoute === '/'
                  ? 'bg-[#F2EDE4] text-[#1B1917]'
                  : 'text-[#5A544E] hover:bg-[#F2EDE4]/60 hover:text-[#1B1917]'
              }`}
            >
              Home
            </a>
            <a
              href="/about"
              onClick={(e) => {
                e.preventDefault();
                handleLinkClick('/about');
              }}
              className={`block px-3 py-2.5 rounded-md text-sm font-medium ${
                currentRoute === '/about'
                  ? 'bg-[#F2EDE4] text-[#1B1917]'
                  : 'text-[#5A544E] hover:bg-[#F2EDE4]/60 hover:text-[#1B1917]'
              }`}
            >
              About Us
            </a>
            <a
              href="/contact"
              onClick={(e) => {
                e.preventDefault();
                handleLinkClick('/contact');
              }}
              className={`block px-3 py-2.5 rounded-md text-sm font-medium ${
                currentRoute === '/contact'
                  ? 'bg-[#F2EDE4] text-[#1B1917]'
                  : 'text-[#5A544E] hover:bg-[#F2EDE4]/60 hover:text-[#1B1917]'
              }`}
            >
              Contact Us
            </a>
          </div>

          <div className="mt-4 pt-4 border-t border-[#DFD6C7]">
            <p className="px-3 mb-2 text-xs font-semibold uppercase tracking-wider text-[#7D5D26]">
              Showroom Collections
            </p>
            <div className="grid grid-cols-1 gap-1">
              {CATEGORIES.map((category) => (
                <a
                  key={category.id}
                  href={category.route}
                  onClick={(e) => {
                    e.preventDefault();
                    handleLinkClick(category.route);
                  }}
                  className={`block px-3 py-2.5 rounded-md text-sm ${
                    currentRoute === category.route
                      ? 'bg-[#F2EDE4] text-[#1B1917] font-semibold'
                      : 'text-[#5A544E] hover:bg-[#F2EDE4]/60 hover:text-[#1B1917]'
                  }`}
                >
                  {category.title}
                </a>
              ))}
            </div>
          </div>

          <div className="mt-5 pt-4 border-t border-[#DFD6C7] space-y-2.5">
            <a
              href={whatsappUrl}
              target="_blank"
              rel="noopener noreferrer"
              className="flex items-center justify-center gap-2 w-full px-4 py-3 text-sm font-semibold bg-[#1B1917] text-[#FAF8F5] rounded-md"
            >
              <MessageCircle className="w-4 h-4 text-[#D4AF6A]" aria-hidden="true" />
              <span>Enquire on WhatsApp</span>
            </a>

            <button
              type="button"
              onClick={() => setMobileMenuOpen(false)}
              className="w-full px-4 py-2.5 text-xs font-medium border border-[#DFD6C7] text-[#5A544E] rounded-md hover:bg-[#F2EDE4] hover:text-[#1B1917] cursor-pointer"
            >
              Close Menu
            </button>
          </div>
        </nav>
      )}
    </header>
  );
}
import { Phone, MessageCircle, MapPin, Clock, Mail, SlidersHorizontal } from 'lucide-react';
import { CATEGORIES } from '../data/catalogue';
import { BRAND_LOGO_URL } from '../data/media';
import {
  formatFullAddress,
  hasConfiguredEmail,
  hasConfiguredHours,
  type BusinessConfig,
} from '../config/businessConfig';
import type { PageRoute } from '../utils/catalogueLogic';
import { buildGoogleMapsUrl, buildWhatsAppGeneralUrl } from '../utils/whatsapp';

interface FooterProps {
  onNavigate: (route: PageRoute) => void;
  config: BusinessConfig;
  onOpenSettings: () => void;
}

export function Footer({ onNavigate, config, onOpenSettings }: FooterProps) {
  const fullAddress = formatFullAddress(config);
  const whatsappUrl = buildWhatsAppGeneralUrl(config.whatsappNumber, config.businessName);
  const mapsUrl = buildGoogleMapsUrl(config.mapQuery || fullAddress);
  const showEmail = hasConfiguredEmail(config.email);
  const showHours = hasConfiguredHours(config);

  const handleNav = (e: React.MouseEvent, route: PageRoute) => {
    e.preventDefault();
    onNavigate(route);
  };

  return (
    <footer className="bg-[#1B1917] text-[#FAF8F5] border-t border-[#322E2A]">
      <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-14 lg:py-16">
        <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-10 lg:gap-12">
          {/* Brand Summary */}
          <div className="space-y-4">
            <div className="flex items-center gap-3">
              <img
                src={BRAND_LOGO_URL}
                alt={`${config.businessName} Logo`}
                referrerPolicy="no-referrer"
                className="w-12 h-12 rounded-full object-cover border border-[#D4AF6A]/60 shrink-0"
              />
              <div>
                <p className="font-display text-lg font-semibold text-[#FAF8F5]">
                  {config.businessName}
                </p>
                <p className="text-xs text-[#D4AF6A] tracking-wide">
                  {config.tagline}
                </p>
              </div>
            </div>
            <p className="text-sm text-[#CFC8BE] leading-relaxed">
              A multi-category retail showroom bringing together established brands across
              men’s and women’s fashion, watches, fragrances, accessories, furniture, and
              electronics under one roof.
            </p>
          </div>

          {/* All 7 Collection Pages */}
          <div>
            <h2 className="font-display text-base font-semibold text-[#FAF8F5] mb-4">
              Shop Categories
            </h2>
            <ul className="space-y-2.5 text-sm text-[#CFC8BE]">
              {CATEGORIES.map((category) => (
                <li key={category.id}>
                  <a
                    href={category.route}
                    onClick={(e) => handleNav(e, category.route)}
                    className="hover:text-[#D4AF6A] transition-colors"
                  >
                    {category.title}
                  </a>
                </li>
              ))}
            </ul>
          </div>

          {/* Showroom Links */}
          <div>
            <h2 className="font-display text-base font-semibold text-[#FAF8F5] mb-4">
              Showroom
            </h2>
            <ul className="space-y-2.5 text-sm text-[#CFC8BE]">
              <li>
                <a
                  href="/"
                  onClick={(e) => handleNav(e, '/')}
                  className="hover:text-[#D4AF6A] transition-colors"
                >
                  Home
                </a>
              </li>
              <li>
                <a
                  href="/about"
                  onClick={(e) => handleNav(e, '/about')}
                  className="hover:text-[#D4AF6A] transition-colors"
                >
                  About Us
                </a>
              </li>
              <li>
                <a
                  href="/contact"
                  onClick={(e) => handleNav(e, '/contact')}
                  className="hover:text-[#D4AF6A] transition-colors"
                >
                  Contact &amp; Directions
                </a>
              </li>
              <li>
                <a
                  href={whatsappUrl}
                  target="_blank"
                  rel="noopener noreferrer"
                  className="hover:text-[#D4AF6A] transition-colors inline-flex items-center gap-1.5"
                >
                  <MessageCircle className="w-3.5 h-3.5 text-[#D4AF6A]" aria-hidden="true" />
                  <span>Direct WhatsApp Desk</span>
                </a>
              </li>
            </ul>
          </div>

          {/* Contact & Adjustable Store Details */}
          <div className="space-y-4">
            <h2 className="font-display text-base font-semibold text-[#FAF8F5] mb-4">
              Visit &amp; Contact
            </h2>
            <div className="space-y-3 text-sm text-[#CFC8BE]">
              <div className="flex items-start gap-2.5">
                <MapPin className="w-4 h-4 text-[#D4AF6A] shrink-0 mt-0.5" aria-hidden="true" />
                <div>
                  <p>{fullAddress}</p>
                  <a
                    href={mapsUrl}
                    target="_blank"
                    rel="noopener noreferrer"
                    className="text-xs text-[#D4AF6A] hover:underline mt-1 inline-block"
                  >
                    Open in Google Maps
                  </a>
                </div>
              </div>
              <div className="flex items-center gap-2.5">
                <Phone className="w-4 h-4 text-[#D4AF6A] shrink-0" aria-hidden="true" />
                <a
                  href={`tel:${config.phoneHref}`}
                  className="hover:text-[#D4AF6A] transition-colors tabular-nums"
                >
                  {config.phoneDisplay}
                </a>
              </div>

              {showEmail && (
                <div className="flex items-center gap-2.5">
                  <Mail className="w-4 h-4 text-[#D4AF6A] shrink-0" aria-hidden="true" />
                  <a
                    href={`mailto:${config.email}`}
                    className="hover:text-[#D4AF6A] transition-colors break-all"
                  >
                    {config.email}
                  </a>
                </div>
              )}

              <div className="flex items-start gap-2.5">
                <Clock className="w-4 h-4 text-[#D4AF6A] shrink-0 mt-0.5" aria-hidden="true" />
                <div className="text-xs space-y-1 text-[#CFC8BE]">
                  {showHours ? (
                    <>
                      {config.businessHours.weekdays && <p>{config.businessHours.weekdays}</p>}
                      {config.businessHours.sunday && <p>{config.businessHours.sunday}</p>}
                    </>
                  ) : (
                    <p>Showroom timings available on phone or WhatsApp</p>
                  )}
                </div>
              </div>
            </div>

            <button
              type="button"
              onClick={onOpenSettings}
              className="inline-flex items-center gap-2 px-3.5 py-2 text-xs font-medium border border-[#49433E] text-[#FAF8F5] rounded-md hover:border-[#D4AF6A] hover:text-[#D4AF6A] transition-colors cursor-pointer"
            >
              <SlidersHorizontal className="w-3.5 h-3.5" aria-hidden="true" />
              <span>Store Contact Settings</span>
            </button>
          </div>
        </div>

        <div className="mt-12 pt-8 border-t border-[#322E2A] flex flex-col sm:flex-row items-start sm:items-center justify-between gap-4 text-xs text-[#A79E92]">
          <p>
            © {new Date().getFullYear()} {config.businessName}. Multi-Category Retail Showroom.
          </p>
          <p>
            All brand names and product models displayed belong to their respective manufacturers.
          </p>
        </div>
      </div>
    </footer>
  );
}
import { useState } from 'react';

interface ImageWithFallbackProps {
  src: string;
  alt: string;
  className?: string;
  loading?: 'eager' | 'lazy';
}

export function ImageWithFallback({
  src,
  alt,
  className = '',
  loading = 'lazy',
}: ImageWithFallbackProps) {
  const [hasError, setHasError] = useState(false);

  if (hasError || !src) {
    return (
      <div
        role="img"
        aria-label={alt}
        className={`flex flex-col items-center justify-center bg-[#EFECE6] text-[#5A544E] p-6 text-center ${className}`}
      >
        <svg
          width="32"
          height="32"
          viewBox="0 0 24 24"
          fill="none"
          stroke="currentColor"
          strokeWidth="1.25"
          aria-hidden="true"
          className="mb-2 text-[#A68142]"
        >
          <rect x="3" y="4" width="18" height="16" rx="2" />
          <circle cx="9" cy="10" r="1.5" />
          <path d="M21 16l-5-4.5-4.5 4-2.5-2L3 19" />
        </svg>
        <span className="text-xs font-medium tracking-wide text-[#5A544E] line-clamp-2">
          {alt}
        </span>
      </div>
    );
  }

  return (
    <img
      src={src}
      alt={alt}
      loading={loading}
      referrerPolicy="no-referrer"
      onError={() => setHasError(true)}
      className={className}
    />
  );
}
import { MessageCircle, ArrowUpRight } from 'lucide-react';
import type { ProductItem } from '../utils/catalogueLogic';
import type { BusinessConfig } from '../config/businessConfig';
import { buildWhatsAppProductUrl } from '../utils/whatsapp';
import { ImageWithFallback } from './ImageWithFallback';

interface ProductCardProps {
  product: ProductItem;
  config: BusinessConfig;
  onViewDetails: (product: ProductItem) => void;
}

export function ProductCard({ product, config, onViewDetails }: ProductCardProps) {
  const whatsappHref = buildWhatsAppProductUrl(
    config.whatsappNumber,
    product.name,
    config.businessName
  );

  return (
    <article className="group flex flex-col bg-white border border-[#DFD6C7] rounded-lg overflow-hidden transition-transform duration-200 hover:-translate-y-0.5 hover:shadow-md">
      {/* Product Image */}
      <div className="relative aspect-[4/3] bg-[#F2EDE4] overflow-hidden">
        <ImageWithFallback
          src={product.image}
          alt={`${product.name} — ${product.categoryLabel}`}
          className="w-full h-full object-cover transition-transform duration-300 group-hover:scale-[1.03]"
        />
      </div>

      {/* Card Content */}
      <div className="flex flex-col flex-1 p-5">
        {/* Clean Unboxed Metadata (Zero-Pill Discipline) */}
        <div className="flex items-center flex-wrap gap-1.5 text-xs text-[#7D5D26] font-medium tracking-wide uppercase">
          <span>{product.categoryLabel}</span>
          <span aria-hidden="true">·</span>
          <span>{product.subcategory}</span>
          {product.isSample && (
            <>
              <span aria-hidden="true">·</span>
              <span className="text-[#5A544E] normal-case font-normal">
                Sample Demonstration
              </span>
            </>
          )}
        </div>

        <h3 className="mt-2 font-display text-lg font-semibold text-[#1B1917] leading-snug">
          {product.name}
        </h3>

        <p className="mt-1 text-xs text-[#5A544E] font-medium">
          Brand: {product.brand}
        </p>

        {/* Price displayed only when provided */}
        <p className="mt-2.5 text-sm font-semibold text-[#1B1917] tabular-nums">
          {product.price ? product.price : 'Price & availability on enquiry'}
        </p>

        <p className="mt-2 text-sm text-[#5A544E] leading-relaxed line-clamp-3">
          {product.description}
        </p>

        {/* Specifications Preview where applicable */}
        {product.specifications && product.specifications.length > 0 && (
          <dl className="mt-4 pt-3 border-t border-[#EFECE6] space-y-1.5 text-xs">
            {product.specifications.slice(0, 3).map((spec) => (
              <div key={spec.label} className="flex items-baseline justify-between gap-3">
                <dt className="text-[#5A544E] shrink-0">{spec.label}</dt>
                <dd className="text-[#1B1917] font-medium text-right truncate">
                  {spec.value}
                </dd>
              </div>
            ))}
          </dl>
        )}

        {/* Actions */}
        <div className="mt-auto pt-5 flex items-center gap-2.5">
          <a
            href={whatsappHref}
            target="_blank"
            rel="noopener noreferrer"
            aria-label={`Enquire on WhatsApp about ${product.name}`}
            className="flex-1 inline-flex items-center justify-center gap-2 px-4 py-2.5 text-xs font-semibold bg-[#1B1917] text-[#FAF8F5] rounded-md hover:bg-[#322E2A] transition-colors whitespace-nowrap focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-[#A68142]"
          >
            <MessageCircle className="w-3.5 h-3.5 text-[#D4AF6A] shrink-0" aria-hidden="true" />
            <span>Enquire on WhatsApp</span>
          </a>

          <button
            type="button"
            onClick={() => onViewDetails(product)}
            aria-label={`View details for ${product.name}`}
            className="inline-flex items-center justify-center gap-1 px-3 py-2.5 text-xs font-medium border border-[#DFD6C7] text-[#1B1917] rounded-md hover:bg-[#F2EDE4] transition-colors whitespace-nowrap shrink-0 cursor-pointer"
          >
            <span>Details</span>
            <ArrowUpRight className="w-3.5 h-3.5" aria-hidden="true" />
          </button>
        </div>
      </div>
    </article>
  );
}
import { useEffect } from 'react';
import { X, MessageCircle, Phone } from 'lucide-react';
import type { ProductItem } from '../utils/catalogueLogic';
import type { BusinessConfig } from '../config/businessConfig';
import { buildWhatsAppProductUrl } from '../utils/whatsapp';
import { ImageWithFallback } from './ImageWithFallback';

interface ProductModalProps {
  product: ProductItem | null;
  config: BusinessConfig;
  onClose: () => void;
}

export function ProductModal({ product, config, onClose }: ProductModalProps) {
  useEffect(() => {
    if (!product) return;
    const handleKey = (e: KeyboardEvent) => {
      if (e.key === 'Escape') onClose();
    };
    document.addEventListener('keydown', handleKey);
    return () => document.removeEventListener('keydown', handleKey);
  }, [product, onClose]);

  if (!product) return null;

  const whatsappHref = buildWhatsAppProductUrl(
    config.whatsappNumber,
    product.name,
    config.businessName
  );

  return (
    <div
      role="dialog"
      aria-modal="true"
      aria-labelledby="product-modal-title"
      className="fixed inset-0 z-50 flex items-center justify-center p-4 bg-[#1B1917]/70 backdrop-blur-xs"
      onClick={onClose}
    >
      <div
        className="relative w-full max-w-3xl bg-[#FAF8F5] border border-[#DFD6C7] rounded-xl overflow-hidden shadow-2xl max-h-[90vh] overflow-y-auto"
        onClick={(e) => e.stopPropagation()}
      >
        <button
          type="button"
          onClick={onClose}
          aria-label="Close product details"
          className="absolute top-4 right-4 z-10 inline-flex items-center justify-center w-10 h-10 rounded-full bg-white/95 border border-[#DFD6C7] text-[#1B1917] hover:bg-[#F2EDE4] transition-colors cursor-pointer"
        >
          <X className="w-4 h-4" aria-hidden="true" />
        </button>

        <div className="grid grid-cols-1 md:grid-cols-2">
          <div className="bg-[#F2EDE4] aspect-[4/3] md:aspect-auto md:h-full">
            <ImageWithFallback
              src={product.image}
              alt={product.name}
              className="w-full h-full object-cover"
              loading="eager"
            />
          </div>

          <div className="p-6 sm:p-8 flex flex-col">
            <div className="flex items-center flex-wrap gap-1.5 text-xs text-[#7D5D26] font-medium uppercase tracking-wide pr-8">
              <span>{product.categoryLabel}</span>
              <span aria-hidden="true">·</span>
              <span>{product.subcategory}</span>
            </div>

            <h2
              id="product-modal-title"
              className="mt-2 font-display text-2xl font-semibold text-[#1B1917]"
            >
              {product.name}
            </h2>

            <p className="mt-1 text-sm text-[#5A544E]">
              Brand: <span className="font-medium text-[#1B1917]">{product.brand}</span>
            </p>

            <p className="mt-3 text-base font-semibold text-[#1B1917] tabular-nums">
              {product.price ? product.price : 'Price & stock shared on WhatsApp / in-store'}
            </p>

            <p className="mt-4 text-sm text-[#5A544E] leading-relaxed">
              {product.description}
            </p>

            {product.specifications && product.specifications.length > 0 && (
              <div className="mt-5 pt-4 border-t border-[#DFD6C7]">
                <h3 className="text-xs font-semibold uppercase tracking-wider text-[#1B1917] mb-2.5">
                  Product Specifications
                </h3>
                <dl className="space-y-2 text-sm">
                  {product.specifications.map((spec) => (
                    <div
                      key={spec.label}
                      className="flex items-baseline justify-between gap-4 border-b border-[#EFECE6] pb-1.5"
                    >
                      <dt className="text-[#5A544E]">{spec.label}</dt>
                      <dd className="text-[#1B1917] font-medium text-right">{spec.value}</dd>
                    </div>
                  ))}
                </dl>
              </div>
            )}

            {product.isSample && (
              <p className="mt-5 p-3 rounded-md bg-[#F2EDE4] text-xs text-[#5A544E] leading-relaxed">
                Demonstration entry: Replace this sample item in{' '}
                <code className="text-[#1B1917]">src/data/catalogue.ts</code> with actual
                brand model, photograph, and showroom pricing.
              </p>
            )}

            <div className="mt-6 pt-4 border-t border-[#DFD6C7] flex flex-wrap gap-3">
              <a
                href={whatsappHref}
                target="_blank"
                rel="noopener noreferrer"
                className="flex-1 inline-flex items-center justify-center gap-2 px-5 py-3 text-xs sm:text-sm font-semibold bg-[#1B1917] text-[#FAF8F5] rounded-md hover:bg-[#322E2A] transition-colors whitespace-nowrap shrink-0"
              >
                <MessageCircle className="w-4 h-4 text-[#D4AF6A] shrink-0" aria-hidden="true" />
                <span>Enquire on WhatsApp</span>
              </a>

              <a
                href={`tel:${config.phoneHref}`}
                className="inline-flex items-center justify-center gap-2 px-4 py-3 text-xs sm:text-sm font-medium border border-[#DFD6C7] text-[#1B1917] rounded-md hover:bg-[#F2EDE4] transition-colors whitespace-nowrap shrink-0"
              >
                <Phone className="w-4 h-4 shrink-0" aria-hidden="true" />
                <span>Call Showroom</span>
              </a>
            </div>
          </div>
        </div>
      </div>
    </div>
  );
}
import { useState, useEffect } from 'react';
import { X, RotateCcw, Check, Download, Loader2 } from 'lucide-react';
import {
  DEFAULT_BUSINESS_CONFIG,
  toEditableBusinessFields,
  type BusinessConfig,
  type EditableBusinessFields,
} from '../config/businessConfig';
import { validateStoreSettings } from '../utils/catalogueLogic';

interface StoreSettingsModalProps {
  isOpen: boolean;
  config: BusinessConfig;
  onSave: (fields: EditableBusinessFields) => void;
  onReset: () => void;
  onClose: () => void;
}

export function StoreSettingsModal({
  isOpen,
  config,
  onSave,
  onReset,
  onClose,
}: StoreSettingsModalProps) {
  const [businessName, setBusinessName] = useState(config.businessName);
  const [tagline, setTagline] = useState(config.tagline);
  const [phoneDisplay, setPhoneDisplay] = useState(config.phoneDisplay);
  const [whatsappNumber, setWhatsappNumber] = useState(config.whatsappNumber);
  const [addressLine1, setAddressLine1] = useState(config.addressLine1);
  const [addressLine2, setAddressLine2] = useState(config.addressLine2);
  const [cityStatePostal, setCityStatePostal] = useState(config.cityStatePostal);
  const [mapQuery, setMapQuery] = useState(config.mapQuery);
  const [email, setEmail] = useState(config.email);
  const [weekdaysHours, setWeekdaysHours] = useState(config.businessHours.weekdays);
  const [sundayHours, setSundayHours] = useState(config.businessHours.sunday);
  const [error, setError] = useState('');
  const [isSaving, setIsSaving] = useState(false);

  useEffect(() => {
    if (isOpen) {
      setBusinessName(config.businessName);
      setTagline(config.tagline);
      setPhoneDisplay(config.phoneDisplay);
      setWhatsappNumber(config.whatsappNumber);
      setAddressLine1(config.addressLine1);
      setAddressLine2(config.addressLine2);
      setCityStatePostal(config.cityStatePostal);
      setMapQuery(config.mapQuery);
      setEmail(config.email);
      setWeekdaysHours(config.businessHours.weekdays);
      setSundayHours(config.businessHours.sunday);
      setError('');
      setIsSaving(false);
    }
  }, [isOpen, config]);

  useEffect(() => {
    if (!isOpen) return;
    const handleEsc = (e: KeyboardEvent) => {
      if (e.key === 'Escape') onClose();
    };
    document.addEventListener('keydown', handleEsc);
    return () => document.removeEventListener('keydown', handleEsc);
  }, [isOpen, onClose]);

  if (!isOpen) return null;

  const buildFieldsPayload = (): EditableBusinessFields => ({
    businessName: businessName.trim(),
    tagline: tagline.trim(),
    phoneDisplay: phoneDisplay.trim(),
    whatsappNumber: whatsappNumber.replace(/\D/g, ''),
    email: email.trim(),
    addressLine1: addressLine1.trim(),
    addressLine2: addressLine2.trim(),
    cityStatePostal: cityStatePostal.trim(),
    mapQuery:
      mapQuery.trim() ||
      [addressLine1.trim(), cityStatePostal.trim()].filter(Boolean).join(', '),
    weekdaysHours: weekdaysHours.trim(),
    sundayHours: sundayHours.trim(),
  });

  const handleSubmit = (e: React.FormEvent) => {
    e.preventDefault();
    const validationError = validateStoreSettings({
      businessName,
      phoneDisplay,
      whatsappNumber,
      email,
      addressLine1,
    });
    if (validationError) {
      setError(validationError);
      return;
    }

    setError('');
    setIsSaving(true);
    window.setTimeout(() => {
      onSave(buildFieldsPayload());
      setIsSaving(false);
      onClose();
    }, 220);
  };

  const handleReset = () => {
    onReset();
    const defaults = toEditableBusinessFields(DEFAULT_BUSINESS_CONFIG);
    setBusinessName(defaults.businessName);
    setTagline(defaults.tagline);
    setPhoneDisplay(defaults.phoneDisplay);
    setWhatsappNumber(defaults.whatsappNumber);
    setAddressLine1(defaults.addressLine1);
    setAddressLine2(defaults.addressLine2);
    setCityStatePostal(defaults.cityStatePostal);
    setMapQuery(defaults.mapQuery);
    setEmail(defaults.email);
    setWeekdaysHours(defaults.weekdaysHours);
    setSundayHours(defaults.sundayHours);
    setError('');
  };

  const handleDownloadJson = () => {
    const validationError = validateStoreSettings({
      businessName,
      phoneDisplay,
      whatsappNumber,
      email,
      addressLine1,
    });
    if (validationError) {
      setError(validationError);
      return;
    }
    const payload = buildFieldsPayload();
    const blob = new Blob([JSON.stringify(payload, null, 2)], {
      type: 'application/json',
    });
    const url = URL.createObjectURL(blob);
    const link = document.createElement('a');
    link.href = url;
    link.download = 'business-config.json';
    document.body.appendChild(link);
    link.click();
    document.body.removeChild(link);
    URL.revokeObjectURL(url);
  };

  return (
    <div
      role="dialog"
      aria-modal="true"
      aria-labelledby="store-settings-title"
      className="fixed inset-0 z-50 flex items-center justify-center p-4 bg-[#1B1917]/70 backdrop-blur-xs"
      onClick={onClose}
    >
      <div
        className="w-full max-w-2xl bg-[#FAF8F5] border border-[#DFD6C7] rounded-xl shadow-2xl max-h-[90vh] overflow-y-auto p-6 sm:p-8"
        onClick={(e) => e.stopPropagation()}
      >
        <div className="flex items-start justify-between gap-4 pb-4 border-b border-[#DFD6C7]">
          <div>
            <h2
              id="store-settings-title"
              className="font-display text-2xl font-semibold text-[#1B1917]"
            >
              Adjust Contact, WhatsApp &amp; Business Details
            </h2>
            <p className="mt-1 text-sm text-[#5A544E]">
              Edit showroom information without changing website code. Save for immediate live
              updates or export <code className="text-[#1B1917]">business-config.json</code>{' '}
              to publish permanently on your host.
            </p>
          </div>
          <button
            type="button"
            onClick={onClose}
            aria-label="Close store settings"
            className="inline-flex items-center justify-center w-9 h-9 rounded-md border border-[#DFD6C7] text-[#1B1917] hover:bg-[#F2EDE4] cursor-pointer shrink-0"
          >
            <X className="w-4 h-4" aria-hidden="true" />
          </button>
        </div>

        <form onSubmit={handleSubmit} noValidate className="mt-5 space-y-4">
          {error && (
            <div
              role="alert"
              className="p-3 rounded-md bg-red-50 border border-red-200 text-xs text-red-800"
            >
              {error}
            </div>
          )}

          <div className="grid grid-cols-1 sm:grid-cols-2 gap-4">
            <div>
              <label
                htmlFor="cfg-name"
                className="block text-xs font-semibold text-[#1B1917] mb-1.5"
              >
                Business Name
              </label>
              <input
                id="cfg-name"
                type="text"
                value={businessName}
                onChange={(e) => setBusinessName(e.target.value)}
                className="w-full px-3.5 py-2.5 text-sm bg-white border border-[#DFD6C7] rounded-md text-[#1B1917] focus:outline-none focus:border-[#A68142]"
              />
            </div>

            <div>
              <label
                htmlFor="cfg-tagline"
                className="block text-xs font-semibold text-[#1B1917] mb-1.5"
              >
                Showroom Tagline
              </label>
              <input
                id="cfg-tagline"
                type="text"
                value={tagline}
                onChange={(e) => setTagline(e.target.value)}
                className="w-full px-3.5 py-2.5 text-sm bg-white border border-[#DFD6C7] rounded-md text-[#1B1917] focus:outline-none focus:border-[#A68142]"
              />
            </div>
          </div>

          <div className="grid grid-cols-1 sm:grid-cols-2 gap-4">
            <div>
              <label
                htmlFor="cfg-phone"
                className="block text-xs font-semibold text-[#1B1917] mb-1.5"
              >
                Contact Phone Number
              </label>
              <input
                id="cfg-phone"
                type="text"
                value={phoneDisplay}
                onChange={(e) => setPhoneDisplay(e.target.value)}
                placeholder="+91 62680 57508"
                className="w-full px-3.5 py-2.5 text-sm bg-white border border-[#DFD6C7] rounded-md text-[#1B1917] focus:outline-none focus:border-[#A68142]"
              />
            </div>

            <div>
              <label
                htmlFor="cfg-whatsapp"
                className="block text-xs font-semibold text-[#1B1917] mb-1.5"
              >
                WhatsApp Number (digits with country code)
              </label>
              <input
                id="cfg-whatsapp"
                type="text"
                value={whatsappNumber}
                onChange={(e) => setWhatsappNumber(e.target.value)}
                placeholder="916268057508"
                className="w-full px-3.5 py-2.5 text-sm bg-white border border-[#DFD6C7] rounded-md text-[#1B1917] focus:outline-none focus:border-[#A68142]"
              />
            </div>
          </div>

          <div>
            <label
              htmlFor="cfg-addr1"
              className="block text-xs font-semibold text-[#1B1917] mb-1.5"
            >
              Showroom Address Line 1
            </label>
            <input
              id="cfg-addr1"
              type="text"
              value={addressLine1}
              onChange={(e) => setAddressLine1(e.target.value)}
              placeholder="Gol Bazar, Devarhat"
              className="w-full px-3.5 py-2.5 text-sm bg-white border border-[#DFD6C7] rounded-md text-[#1B1917] focus:outline-none focus:border-[#A68142]"
            />
          </div>

          <div className="grid grid-cols-1 sm:grid-cols-2 gap-4">
            <div>
              <label
                htmlFor="cfg-addr2"
                className="block text-xs font-semibold text-[#1B1917] mb-1.5"
              >
                Landmark / Regional Address (Optional)
              </label>
              <input
                id="cfg-addr2"
                type="text"
                value={addressLine2}
                onChange={(e) => setAddressLine2(e.target.value)}
                placeholder="गोल बाजार, देवरहट"
                className="w-full px-3.5 py-2.5 text-sm bg-white border border-[#DFD6C7] rounded-md text-[#1B1917] focus:outline-none focus:border-[#A68142]"
              />
            </div>

            <div>
              <label
                htmlFor="cfg-city"
                className="block text-xs font-semibold text-[#1B1917] mb-1.5"
              >
                District, State &amp; PIN Code (Optional)
              </label>
              <input
                id="cfg-city"
                type="text"
                value={cityStatePostal}
                onChange={(e) => setCityStatePostal(e.target.value)}
                placeholder="District, State - PIN"
                className="w-full px-3.5 py-2.5 text-sm bg-white border border-[#DFD6C7] rounded-md text-[#1B1917] focus:outline-none focus:border-[#A68142]"
              />
            </div>
          </div>

          <div className="grid grid-cols-1 sm:grid-cols-2 gap-4">
            <div>
              <label
                htmlFor="cfg-email"
                className="block text-xs font-semibold text-[#1B1917] mb-1.5"
              >
                Business Email (Leave empty to hide)
              </label>
              <input
                id="cfg-email"
                type="email"
                value={email}
                onChange={(e) => setEmail(e.target.value)}
                placeholder="Leave blank until official email is ready"
                className="w-full px-3.5 py-2.5 text-sm bg-white border border-[#DFD6C7] rounded-md text-[#1B1917] focus:outline-none focus:border-[#A68142]"
              />
            </div>

            <div>
              <label
                htmlFor="cfg-map"
                className="block text-xs font-semibold text-[#1B1917] mb-1.5"
              >
                Google Maps Search Query
              </label>
              <input
                id="cfg-map"
                type="text"
                value={mapQuery}
                onChange={(e) => setMapQuery(e.target.value)}
                placeholder="Gol Bazar, Devarhat"
                className="w-full px-3.5 py-2.5 text-sm bg-white border border-[#DFD6C7] rounded-md text-[#1B1917] focus:outline-none focus:border-[#A68142]"
              />
            </div>
          </div>

          <div className="grid grid-cols-1 sm:grid-cols-2 gap-4">
            <div>
              <label
                htmlFor="cfg-hours1"
                className="block text-xs font-semibold text-[#1B1917] mb-1.5"
              >
                Weekday Opening Hours (Optional)
              </label>
              <input
                id="cfg-hours1"
                type="text"
                value={weekdaysHours}
                onChange={(e) => setWeekdaysHours(e.target.value)}
                placeholder="e.g. Mon – Sat: 10:00 AM – 9:00 PM"
                className="w-full px-3.5 py-2.5 text-sm bg-white border border-[#DFD6C7] rounded-md text-[#1B1917] focus:outline-none focus:border-[#A68142]"
              />
            </div>

            <div>
              <label
                htmlFor="cfg-hours2"
                className="block text-xs font-semibold text-[#1B1917] mb-1.5"
              >
                Sunday Opening Hours (Optional)
              </label>
              <input
                id="cfg-hours2"
                type="text"
                value={sundayHours}
                onChange={(e) => setSundayHours(e.target.value)}
                placeholder="e.g. Sunday: 11:00 AM – 8:00 PM"
                className="w-full px-3.5 py-2.5 text-sm bg-white border border-[#DFD6C7] rounded-md text-[#1B1917] focus:outline-none focus:border-[#A68142]"
              />
            </div>
          </div>

          <div className="pt-4 border-t border-[#DFD6C7] flex flex-col sm:flex-row flex-wrap items-stretch sm:items-center justify-between gap-3">
            <div className="flex flex-wrap items-center gap-2">
              <button
                type="button"
                onClick={handleReset}
                className="inline-flex items-center justify-center gap-2 px-3.5 py-2.5 text-xs font-medium border border-[#DFD6C7] text-[#5A544E] rounded-md hover:bg-[#F2EDE4] hover:text-[#1B1917] transition-colors cursor-pointer"
              >
                <RotateCcw className="w-3.5 h-3.5" aria-hidden="true" />
                <span>Reset Defaults</span>
              </button>

              <button
                type="button"
                onClick={handleDownloadJson}
                className="inline-flex items-center justify-center gap-2 px-3.5 py-2.5 text-xs font-medium border border-[#DFD6C7] bg-white text-[#1B1917] rounded-md hover:bg-[#F2EDE4] transition-colors cursor-pointer"
              >
                <Download className="w-3.5 h-3.5 text-[#7D5D26]" aria-hidden="true" />
                <span>Download JSON</span>
              </button>
            </div>

            <div className="flex items-center justify-end gap-3">
              <button
                type="button"
                onClick={onClose}
                className="px-4 py-2.5 text-xs font-medium text-[#5A544E] hover:text-[#1B1917] cursor-pointer"
              >
                Cancel
              </button>
              <button
                type="submit"
                disabled={isSaving}
                className="inline-flex items-center justify-center gap-2 px-5 py-2.5 text-xs font-semibold bg-[#1B1917] text-[#FAF8F5] rounded-md hover:bg-[#322E2A] disabled:opacity-70 transition-colors cursor-pointer whitespace-nowrap"
              >
                {isSaving ? (
                  <>
                    <Loader2 className="w-3.5 h-3.5 animate-spin text-[#D4AF6A]" aria-hidden="true" />
                    <span>Saving Details...</span>
                  </>
                ) : (
                  <>
                    <Check className="w-3.5 h-3.5 text-[#D4AF6A]" aria-hidden="true" />
                    <span>Save Showroom Details</span>
                  </>
                )}
              </button>
            </div>
          </div>
        </form>
      </div>
    </div>
  );
}
import { ArrowRight, MapPin, Phone, MessageCircle, Clock, Mail, SlidersHorizontal } from 'lucide-react';
import { CATEGORIES, SAMPLE_PRODUCTS } from '../data/catalogue';
import { SHOWROOM_MEDIA } from '../data/media';
import {
  formatFullAddress,
  hasConfiguredEmail,
  hasConfiguredHours,
  type BusinessConfig,
} from '../config/businessConfig';
import {
  getFeaturedProducts,
  type PageRoute,
  type ProductItem,
} from '../utils/catalogueLogic';
import {
  buildGoogleMapsEmbedUrl,
  buildGoogleMapsUrl,
  buildWhatsAppGeneralUrl,
} from '../utils/whatsapp';
import { ImageWithFallback } from '../components/ImageWithFallback';
import { ProductCard } from '../components/ProductCard';

interface HomePageProps {
  config: BusinessConfig;
  onNavigate: (route: PageRoute) => void;
  onSelectProduct: (product: ProductItem) => void;
  onOpenSettings: () => void;
}

const VERIFIABLE_REASONS = [
  {
    number: '01',
    title: 'Multiple Brands Under One Roof',
    description:
      'Compare styles, fits, finishes, and models from different established brands and manufacturers in a single showroom visit.',
  },
  {
    number: '02',
    title: 'Apparel, Home & Electronics Together',
    description:
      'Shop across men’s and women’s clothing, watches, perfumes, accessories, furniture, and home electronics without visiting separate stores.',
  },
  {
    number: '03',
    title: 'In-Person Inspection & Guidance',
    description:
      'Examine fabric weights, furniture upholstery, watch dials, and appliance specifications firsthand with assistance from our showroom team.',
  },
  {
    number: '04',
    title: 'Direct WhatsApp Product Enquiry',
    description:
      'Check current showroom availability and pricing for any item on WhatsApp before you plan your visit.',
  },
];

export function HomePage({
  config,
  onNavigate,
  onSelectProduct,
  onOpenSettings,
}: HomePageProps) {
  const featuredProducts = getFeaturedProducts(SAMPLE_PRODUCTS, 6);
  const fullAddress = formatFullAddress(config);
  const mapsUrl = buildGoogleMapsUrl(config.mapQuery || fullAddress);
  const mapsEmbedUrl = buildGoogleMapsEmbedUrl(config.mapQuery || fullAddress);
  const whatsappUrl = buildWhatsAppGeneralUrl(config.whatsappNumber, config.businessName);
  const showEmail = hasConfiguredEmail(config.email);
  const showHours = hasConfiguredHours(config);

  const scrollToCategories = () => {
    const el = document.getElementById('shop-by-category');
    if (el) {
      el.scrollIntoView({ behavior: 'smooth' });
    }
  };

  return (
    <div>
      {/* 1. HERO SECTION */}
      <section className="border-b border-[#DFD6C7] bg-[#FAF8F5]">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-12 lg:py-20">
          <div className="grid grid-cols-1 lg:grid-cols-12 gap-10 lg:gap-12 items-stretch">
            <div className="lg:col-span-5 flex flex-col justify-center">
              <p className="mb-4 text-xs tracking-widest uppercase text-[#7D5D26] font-semibold">
                {config.businessName} · Retail Showroom
              </p>

              <h1 className="font-display text-[clamp(2.25rem,4vw,3.65rem)] font-semibold leading-[1.1] tracking-tight text-[#1B1917] text-balance">
                Style, Comfort &amp; Everything You Need.
              </h1>

              <p className="mt-5 text-base text-[#5A544E] leading-relaxed max-w-xl">
                {config.businessName} is a multi-category retail showroom bringing
                together curated collections from established apparel, timepiece, fragrance,
                furniture, and electronics brands — all thoughtfully displayed in one place.
              </p>

              <div className="mt-8 flex flex-wrap items-center gap-3.5">
                <button
                  type="button"
                  onClick={scrollToCategories}
                  className="inline-flex items-center gap-2 px-6 py-3.5 text-sm font-semibold bg-[#1B1917] text-[#FAF8F5] rounded-md hover:bg-[#322E2A] transition-colors whitespace-nowrap cursor-pointer focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-[#A68142]"
                >
                  <span>Explore Collections</span>
                  <ArrowRight className="w-4 h-4 text-[#D4AF6A]" aria-hidden="true" />
                </button>

                <a
                  href="/contact"
                  onClick={(e) => {
                    e.preventDefault();
                    onNavigate('/contact');
                  }}
                  className="inline-flex items-center gap-2 px-6 py-3.5 text-sm font-medium border border-[#DFD6C7] bg-white text-[#1B1917] rounded-md hover:bg-[#F2EDE4] transition-colors whitespace-nowrap"
                >
                  <span>Contact Us</span>
                </a>
              </div>

              <p className="mt-8 pt-6 border-t border-[#DFD6C7] text-xs text-[#5A544E] leading-relaxed">
                {config.tagline} — Seven curated showroom departments with direct WhatsApp
                enquiry for pricing and current in-store availability.
              </p>
            </div>

            <div className="lg:col-span-7">
              <div className="relative h-full min-h-[280px] sm:min-h-[380px] lg:min-h-[480px] rounded-xl overflow-hidden border border-[#DFD6C7] bg-[#F2EDE4]">
                <ImageWithFallback
                  src={SHOWROOM_MEDIA.heroShowroom}
                  alt={`Interior view of ${config.businessName} multi-category retail showroom`}
                  className="w-full h-full lg:h-full object-cover"
                  loading="eager"
                />
                <div className="absolute inset-x-0 bottom-0 bg-gradient-to-t from-[#1B1917]/95 via-[#1B1917]/65 to-transparent pt-16 p-6 sm:p-8">
                  <p className="text-xs uppercase tracking-widest text-[#E5C78B] font-semibold">
                    Multi-Brand Retail Experience
                  </p>
                  <p className="mt-1.5 font-display text-xl sm:text-2xl text-[#FAF8F5]">
                    Fashion, Accessories, Furniture &amp; Electronics under one roof
                  </p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>

      {/* 2. SHOP BY CATEGORY (ALL 7 CATEGORIES) */}
      <section
        id="shop-by-category"
        className="py-16 lg:py-20 bg-[#F2EDE4]/55 border-b border-[#DFD6C7]"
      >
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div className="flex flex-col md:flex-row md:items-end justify-between gap-4 mb-10">
            <div>
              <p className="text-xs uppercase tracking-widest text-[#7D5D26] font-semibold">
                Showroom Departments
              </p>
              <h2 className="mt-2 font-display text-3xl sm:text-4xl font-semibold text-[#1B1917]">
                Shop by Category
              </h2>
            </div>
            <p className="text-sm text-[#5A544E] max-w-md">
              Browse all seven showroom departments to discover stocked styles, product
              specifications, and enquire directly on WhatsApp.
            </p>
          </div>

          <div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6">
            {CATEGORIES.map((category, index) => (
              <a
                key={category.id}
                href={category.route}
                onClick={(e) => {
                  e.preventDefault();
                  onNavigate(category.route);
                }}
                className={`group flex flex-col bg-white border border-[#DFD6C7] rounded-lg overflow-hidden transition-transform duration-200 hover:-translate-y-0.5 hover:shadow-md ${
                  index === 0 ? 'sm:col-span-2 lg:col-span-2' : ''
                }`}
              >
                <div
                  className={`relative overflow-hidden bg-[#EFECE6] ${
                    index === 0 ? 'aspect-[16/9] sm:aspect-[16/9] lg:aspect-[2/1]' : 'aspect-[4/3]'
                  }`}
                >
                  <ImageWithFallback
                    src={category.heroImage}
                    alt={`${category.title} collection at ${config.businessName}`}
                    className="w-full h-full object-cover transition-transform duration-300 group-hover:scale-[1.03]"
                  />
                </div>
                <div className="p-5 flex-1 flex flex-col justify-between">
                  <div>
                    <p className="text-xs text-[#7D5D26] font-medium uppercase tracking-wider">
                      0{index + 1} · Department
                    </p>
                    <h3 className="mt-1.5 font-display text-xl font-semibold text-[#1B1917]">
                      {category.title}
                    </h3>
                    <p className="mt-1.5 text-sm text-[#5A544E] leading-relaxed">
                      {category.tagline}
                    </p>
                  </div>
                  <div className="mt-4 pt-3 border-t border-[#EFECE6] inline-flex items-center gap-1.5 text-xs font-semibold text-[#1B1917] group-hover:text-[#7D5D26] transition-colors">
                    <span>Explore {category.shortTitle}</span>
                    <ArrowRight className="w-3.5 h-3.5" aria-hidden="true" />
                  </div>
                </div>
              </a>
            ))}
          </div>
        </div>
      </section>

      {/* 3. FEATURED COLLECTIONS */}
      <section className="py-16 lg:py-20 bg-[#FAF8F5] border-b border-[#DFD6C7]">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div className="flex flex-col md:flex-row md:items-end justify-between gap-4 mb-10">
            <div>
              <p className="text-xs uppercase tracking-widest text-[#7D5D26] font-semibold">
                Demonstration Showcase
              </p>
              <h2 className="mt-2 font-display text-3xl sm:text-4xl font-semibold text-[#1B1917]">
                Featured Collections
              </h2>
            </div>
            <p className="text-sm text-[#5A544E] max-w-lg">
              Initial sample demonstration items across fashion, watches, fragrances,
              accessories, furniture, and electronics. Replace with your live showroom stock
              in <code className="text-[#1B1917]">src/data/catalogue.ts</code>.
            </p>
          </div>

          {featuredProducts.length > 0 ? (
            <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-7">
              {featuredProducts.map((product) => (
                <ProductCard
                  key={product.id}
                  product={product}
                  config={config}
                  onViewDetails={onSelectProduct}
                />
              ))}
            </div>
          ) : (
            <div className="p-8 text-center bg-white border border-[#DFD6C7] rounded-lg">
              <p className="text-sm text-[#5A544E]">
                Live product listings are being updated. Contact our showroom on WhatsApp for
                current brands and availability.
              </p>
            </div>
          )}
        </div>
      </section>

      {/* 4. OUR SHOWROOM & WHY SHOP WITH US */}
      <section className="py-16 lg:py-20 bg-[#F2EDE4]/55 border-b border-[#DFD6C7]">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div className="grid grid-cols-1 lg:grid-cols-12 gap-12 items-start">
            <div className="lg:col-span-5 space-y-5">
              <p className="text-xs uppercase tracking-widest text-[#7D5D26] font-semibold">
                Our Showroom
              </p>
              <h2 className="font-display text-3xl sm:text-4xl font-semibold text-[#1B1917] text-balance">
                One Retail Destination for Apparel, Living &amp; Home Tech
              </h2>
              <p className="text-base text-[#5A544E] leading-relaxed">
                As a multi-category retail showroom, {config.businessName} curates
                products from established brands and independent manufacturers rather than
                selling a single proprietary label.
              </p>
              <p className="text-base text-[#5A544E] leading-relaxed">
                Whether you are updating everyday wardrobes, choosing a gift watch or fragrance,
                furnishing a living room, or comparing electronics models, our layout is
                organized for straightforward product discovery.
              </p>
              <div className="pt-2">
                <a
                  href="/about"
                  onClick={(e) => {
                    e.preventDefault();
                    onNavigate('/about');
                  }}
                  className="inline-flex items-center gap-2 text-sm font-semibold text-[#1B1917] hover:text-[#7D5D26] transition-colors"
                >
                  <span>Read more about our showroom</span>
                  <ArrowRight className="w-4 h-4" aria-hidden="true" />
                </a>
              </div>
            </div>

            <div className="lg:col-span-7">
              <h3 className="font-display text-2xl font-semibold text-[#1B1917] mb-6">
                Why Shop With Us
              </h3>
              <div className="grid grid-cols-1 sm:grid-cols-2 gap-6">
                {VERIFIABLE_REASONS.map((item) => (
                  <div
                    key={item.number}
                    className="p-6 bg-white border border-[#DFD6C7] rounded-lg"
                  >
                    <p className="text-xs font-semibold text-[#7D5D26] tabular-nums">
                      {item.number}.
                    </p>
                    <h4 className="mt-2 font-display text-lg font-semibold text-[#1B1917]">
                      {item.title}
                    </h4>
                    <p className="mt-2 text-sm text-[#5A544E] leading-relaxed">
                      {item.description}
                    </p>
                  </div>
                ))}
              </div>
            </div>
          </div>
        </div>
      </section>

      {/* 5. CONTACT SECTION */}
      <section className="py-16 lg:py-20 bg-[#FAF8F5]">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div className="flex flex-col md:flex-row md:items-end justify-between gap-4 mb-10">
            <div>
              <p className="text-xs uppercase tracking-widest text-[#7D5D26] font-semibold">
                Plan Your Visit
              </p>
              <h2 className="mt-2 font-display text-3xl sm:text-4xl font-semibold text-[#1B1917]">
                Visit or Message the Showroom
              </h2>
            </div>

            <button
              type="button"
              onClick={onOpenSettings}
              className="inline-flex items-center gap-2 px-4 py-2.5 text-xs font-semibold border border-[#DFD6C7] bg-white text-[#1B1917] rounded-md hover:bg-[#F2EDE4] transition-colors cursor-pointer self-start md:self-auto"
            >
              <SlidersHorizontal className="w-3.5 h-3.5 text-[#7D5D26]" aria-hidden="true" />
              <span>Edit Contact, WhatsApp &amp; Address</span>
            </button>
          </div>

          <div className="grid grid-cols-1 lg:grid-cols-12 gap-8 items-stretch">
            <div className="lg:col-span-5 bg-white border border-[#DFD6C7] rounded-lg p-6 sm:p-8 flex flex-col justify-between space-y-6">
              <div className="space-y-5">
                <div className="flex items-start gap-3.5">
                  <Phone className="w-5 h-5 text-[#7D5D26] shrink-0 mt-0.5" aria-hidden="true" />
                  <div>
                    <p className="text-xs uppercase tracking-wider text-[#5A544E] font-medium">
                      Phone Number
                    </p>
                    <a
                      href={`tel:${config.phoneHref}`}
                      className="mt-1 block text-base font-semibold text-[#1B1917] hover:text-[#7D5D26] tabular-nums"
                    >
                      {config.phoneDisplay}
                    </a>
                  </div>
                </div>

                <div className="flex items-start gap-3.5">
                  <MessageCircle
                    className="w-5 h-5 text-[#7D5D26] shrink-0 mt-0.5"
                    aria-hidden="true"
                  />
                  <div>
                    <p className="text-xs uppercase tracking-wider text-[#5A544E] font-medium">
                      WhatsApp Enquiry Desk
                    </p>
                    <p className="mt-1 text-base font-semibold text-[#1B1917] tabular-nums">
                      +{config.whatsappNumber}
                    </p>
                  </div>
                </div>

                {showEmail && (
                  <div className="flex items-start gap-3.5">
                    <Mail className="w-5 h-5 text-[#7D5D26] shrink-0 mt-0.5" aria-hidden="true" />
                    <div>
                      <p className="text-xs uppercase tracking-wider text-[#5A544E] font-medium">
                        Email
                      </p>
                      <a
                        href={`mailto:${config.email}`}
                        className="mt-1 block text-sm font-medium text-[#1B1917] hover:text-[#7D5D26] break-all"
                      >
                        {config.email}
                      </a>
                    </div>
                  </div>
                )}

                <div className="flex items-start gap-3.5">
                  <MapPin className="w-5 h-5 text-[#7D5D26] shrink-0 mt-0.5" aria-hidden="true" />
                  <div>
                    <p className="text-xs uppercase tracking-wider text-[#5A544E] font-medium">
                      Showroom Address
                    </p>
                    <p className="mt-1 text-sm text-[#1B1917] leading-relaxed">
                      {fullAddress}
                    </p>
                    <a
                      href={mapsUrl}
                      target="_blank"
                      rel="noopener noreferrer"
                      className="mt-1.5 inline-block text-xs font-semibold text-[#7D5D26] hover:underline"
                    >
                      View directions on Google Maps
                    </a>
                  </div>
                </div>

                <div className="flex items-start gap-3.5">
                  <Clock className="w-5 h-5 text-[#7D5D26] shrink-0 mt-0.5" aria-hidden="true" />
                  <div>
                    <p className="text-xs uppercase tracking-wider text-[#5A544E] font-medium">
                      Business Hours
                    </p>
                    {showHours ? (
                      <>
                        {config.businessHours.weekdays && (
                          <p className="mt-1 text-sm text-[#1B1917]">
                            {config.businessHours.weekdays}
                          </p>
                        )}
                        {config.businessHours.sunday && (
                          <p className="mt-0.5 text-sm text-[#5A544E]">
                            {config.businessHours.sunday}
                          </p>
                        )}
                      </>
                    ) : (
                      <p className="mt-1 text-sm text-[#5A544E]">
                        Opening hours confirmed by phone or WhatsApp (editable in Store
                        Settings).
                      </p>
                    )}
                  </div>
                </div>
              </div>

              <div className="pt-4 border-t border-[#EFECE6] flex flex-wrap gap-3">
                <a
                  href={whatsappUrl}
                  target="_blank"
                  rel="noopener noreferrer"
                  cla
                  import { ArrowRight, MessageCircle } from 'lucide-react';
import { CATEGORIES } from '../data/catalogue';
import { BRAND_LOGO_URL, SHOWROOM_MEDIA } from '../data/media';
import type { BusinessConfig } from '../config/businessConfig';
import type { PageRoute } from '../utils/catalogueLogic';
import { buildWhatsAppGeneralUrl } from '../utils/whatsapp';
import { ImageWithFallback } from '../components/ImageWithFallback';

interface AboutPageProps {
  config: BusinessConfig;
  onNavigate: (route: PageRoute) => void;
}

export function AboutPage({ config, onNavigate }: AboutPageProps) {
  const whatsappUrl = buildWhatsAppGeneralUrl(config.whatsappNumber, config.businessName);

  return (
    <div className="bg-[#FAF8F5]">
      {/* About Hero */}
      <section className="border-b border-[#DFD6C7] bg-[#F2EDE4]/55">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-14 lg:py-20">
          <div className="grid grid-cols-1 lg:grid-cols-12 gap-10 items-center">
            <div className="lg:col-span-6 space-y-5">
              <div className="flex items-center gap-3">
                <img
                  src={BRAND_LOGO_URL}
                  alt="Sachin Jeans & Furniture Emblem"
                  referrerPolicy="no-referrer"
                  className="w-12 h-12 rounded-full object-cover border border-[#C49B54]/70 shrink-0"
                />
                <p className="text-xs uppercase tracking-widest text-[#7D5D26] font-semibold">
                  About Our Showroom
                </p>
              </div>
              <h1 className="font-display text-3xl sm:text-5xl font-semibold text-[#1B1917] text-balance">
                A Multi-Category Retail Showroom Built Around Convenience &amp; Choice
              </h1>
              <p className="text-base text-[#5A544E] leading-relaxed">
                {config.businessName} operates as a multi-brand retail showroom—bringing
                together apparel, watches, perfumes, fashion accessories, furniture, and
                electronics from different established brands and product manufacturers.
              </p>
              <p className="text-base text-[#5A544E] leading-relaxed">
                We do not manufacture clothing or furniture under a proprietary factory label;
                instead, we focus on curating varied styles, dependable household options, and
                practical product choices in one accessible showroom.
              </p>
            </div>

            <div className="lg:col-span-6">
              <div className="aspect-[16/10] rounded-xl overflow-hidden border border-[#DFD6C7] bg-[#EFECE6]">
                <ImageWithFallback
                  src={SHOWROOM_MEDIA.heroShowroom}
                  alt="Sachin Jeans & Furniture retail showroom gallery"
                  className="w-full h-full object-cover"
                  loading="eager"
                />
              </div>
            </div>
          </div>
        </div>
      </section>

      {/* What We Carry */}
      <section className="py-16 lg:py-20 border-b border-[#DFD6C7]">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div className="max-w-2xl mb-10">
            <p className="text-xs uppercase tracking-widest text-[#7D5D26] font-semibold">
              Departments Under One Roof
            </p>
            <h2 className="mt-2 font-display text-3xl font-semibold text-[#1B1917]">
              Seven Categories Across Wardrobe &amp; Home
            </h2>
          </div>

          <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
            {CATEGORIES.map((cat) => (
              <div
                key={cat.id}
                className="p-6 bg-white border border-[#DFD6C7] rounded-lg flex flex-col justify-between"
              >
                <div>
                  <h3 className="font-display text-xl font-semibold text-[#1B1917]">
                    {cat.title}
                  </h3>
                  <p className="mt-2 text-sm text-[#5A544E] leading-relaxed">
                    {cat.description}
                  </p>
                </div>
                <div className="mt-5 pt-4 border-t border-[#EFECE6]">
                  <a
                    href={cat.route}
                    onClick={(e) => {
                      e.preventDefault();
                      onNavigate(cat.route);
                    }}
                    className="inline-flex items-center gap-1.5 text-xs font-semibold text-[#1B1917] hover:text-[#7D5D26]"
                  >
                    <span>Browse {cat.shortTitle}</span>
                    <ArrowRight className="w-3.5 h-3.5" aria-hidden="true" />
                  </a>
                </div>
              </div>
            ))}
          </div>
        </div>
      </section>

      {/* Customer Assistance */}
      <section className="py-16 bg-[#F2EDE4]/55">
        <div className="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
          <h2 className="font-display text-3xl font-semibold text-[#1B1917]">
            Have a Specific Brand, Size, or Model in Mind?
          </h2>
          <p className="mt-3 text-base text-[#5A544E]">
            Message our showroom desk on WhatsApp or visit us in person to confirm current
            stock, dimensions, and pricing.
          </p>
          <div className="mt-7 flex flex-wrap justify-center gap-3.5">
            <a
              href={whatsappUrl}
              target="_blank"
              rel="noopener noreferrer"
              className="inline-flex items-center gap-2 px-6 py-3 text-sm font-semibold bg-[#1B1917] text-[#FAF8F5] rounded-md hover:bg-[#322E2A]"
            >
              <MessageCircle className="w-4 h-4 text-[#D4AF6A]" aria-hidden="true" />
              <span>Enquire on WhatsApp</span>
            </a>
            <a
              href="/contact"
              onClick={(e) => {
                e.preventDefault();
                onNavigate('/contact');
              }}
              className="inline-flex items-center gap-2 px-6 py-3 text-sm font-medium border border-[#DFD6C7] bg-white text-[#1B1917] rounded-md hover:bg-[#F2EDE4]"
            >
              <span>View Address &amp; Hours</span>
            </a>
          </div>
        </div>
      </section>
    </div>
  );
}
import { useState, useEffect } from 'react';
import { Search, ArrowLeft, X, ArrowUpDown } from 'lucide-react';
import { CATEGORIES, SAMPLE_PRODUCTS } from '../data/catalogue';
import type { BusinessConfig } from '../config/businessConfig';
import {
  filterProducts,
  type CategoryMeta,
  type PageRoute,
  type ProductItem,
  type ProductSortOption,
} from '../utils/catalogueLogic';
import { ImageWithFallback } from '../components/ImageWithFallback';
import { ProductCard } from '../components/ProductCard';

interface CategoryPageProps {
  category: CategoryMeta;
  config: BusinessConfig;
  onNavigate: (route: PageRoute) => void;
  onSelectProduct: (product: ProductItem) => void;
}

export function CategoryPage({
  category,
  config,
  onNavigate,
  onSelectProduct,
}: CategoryPageProps) {
  const [selectedSubcategory, setSelectedSubcategory] = useState<string>('All');
  const [searchQuery, setSearchQuery] = useState<string>('');
  const [sortBy, setSortBy] = useState<ProductSortOption>('featured');
  const [hideDemoItems, setHideDemoItems] = useState<boolean>(false);

  useEffect(() => {
    setSelectedSubcategory('All');
    setSearchQuery('');
    setSortBy('featured');
    setHideDemoItems(false);
  }, [category.id]);

  const filteredProducts = filterProducts(SAMPLE_PRODUCTS, {
    categoryId: category.id,
    subcategory: selectedSubcategory,
    searchQuery,
    sortBy,
    hideDemoItems,
  });

  const hasDemoEntries = filteredProducts.some((p) => p.isSample);
  const hasActiveFilters =
    selectedSubcategory !== 'All' || searchQuery.trim().length > 0 || hideDemoItems;

  const otherCategories = CATEGORIES.filter((c) => c.id !== category.id);

  const resetAllFilters = () => {
    setSelectedSubcategory('All');
    setSearchQuery('');
    setSortBy('featured');
    setHideDemoItems(false);
  };

  return (
    <div className="bg-[#FAF8F5]">
      {/* Department Quick-Switcher Bar */}
      <div className="border-b border-[#DFD6C7] bg-[#FAF8F5]">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-3 overflow-x-auto">
          <nav
            aria-label="Switch showroom department"
            className="flex items-center gap-2 min-w-max"
          >
            {CATEGORIES.map((dept) => {
              const isCurrent = dept.id === category.id;
              return (
                <a
                  key={dept.id}
                  href={dept.route}
                  onClick={(e) => {
                    e.preventDefault();
                    onNavigate(dept.route);
                  }}
                  aria-current={isCurrent ? 'page' : undefined}
                  className={`px-3 py-1.5 text-xs font-medium rounded-md transition-colors whitespace-nowrap shrink-0 ${
                    isCurrent
                      ? 'bg-[#1B1917] text-[#FAF8F5]'
                      : 'text-[#5A544E] hover:bg-[#F2EDE4] hover:text-[#1B1917]'
                  }`}
                >
                  {dept.shortTitle}
                </a>
              );
            })}
          </nav>
        </div>
      </div>

      {/* Category Header */}
      <section className="border-b border-[#DFD6C7] bg-[#F2EDE4]/55">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-10 lg:py-14">
          <nav aria-label="Breadcrumb" className="mb-6">
            <a
              href="/"
              onClick={(e) => {
                e.preventDefault();
                onNavigate('/');
              }}
              className="inline-flex items-center gap-1.5 text-xs font-medium text-[#5A544E] hover:text-[#1B1917] transition-colors"
            >
              <ArrowLeft className="w-3.5 h-3.5" aria-hidden="true" />
              <span>Back to Home</span>
            </a>
          </nav>

          <div className="grid grid-cols-1 lg:grid-cols-12 gap-8 items-center">
            <div className="lg:col-span-7">
              <p className="text-xs uppercase tracking-widest text-[#7D5D26] font-semibold">
                {config.businessName} · Department Catalogue
              </p>
              <h1 className="mt-2 font-display text-3xl sm:text-5xl font-semibold text-[#1B1917] text-balance">
                {category.title}
              </h1>
              <p className="mt-4 text-base text-[#5A544E] leading-relaxed max-w-2xl">
                {category.description}
              </p>
              <p className="mt-4 text-xs text-[#5A544E]">
                Click <strong className="text-[#1B1917]">Enquire on WhatsApp</strong> on any item
                to request current showroom pricing and in-store availability.
              </p>
            </div>

            <div className="lg:col-span-5">
              <div className="aspect-[4/3] rounded-xl overflow-hidden border border-[#DFD6C7] bg-[#EFECE6]">
                <ImageWithFallback
                  src={category.heroImage}
                  alt={category.title}
                  className="w-full h-full object-cover"
                  loading="eager"
                />
              </div>
            </div>
          </div>
        </div>
      </section>

      {/* Filter, Sort & Search Bar */}
      <section className="border-b border-[#DFD6C7] bg-white">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-5 space-y-4">
          <div className="flex flex-col lg:flex-row lg:items-center justify-between gap-4">
            {/* Subcategory Filter Buttons */}
            <div
              role="group"
              aria-label={`Filter ${category.title} by subcategory`}
              className="flex flex-wrap items-center gap-2"
            >
              {category.subcategories.map((sub) => {
                const isActive = selectedSubcategory === sub;
                return (
                  <button
                    key={sub}
                    type="button"
                    onClick={() => setSelectedSubcategory(sub)}
                    aria-pressed={isActive}
                    className={`px-3.5 py-2 text-xs font-medium rounded-md transition-colors whitespace-nowrap shrink-0 cursor-pointer ${
                      isActive
                        ? 'bg-[#1B1917] text-[#FAF8F5]'
                        : 'bg-[#F2EDE4] text-[#5A544E] hover:text-[#1B1917] hover:bg-[#E7E0D3]'
                    }`}
                  >
                    {sub}
                  </button>
                );
              })}
            </div>

            {/* Search & Sort Controls */}
            <div className="flex flex-col sm:flex-row items-stretch sm:items-center gap-3 shrink-0">
              <div className="relative w-full sm:w-64">
                <Search
                  className="w-4 h-4 text-[#5A544E] absolute left-3 top-1/2 -translate-y-1/2 pointer-events-none"
                  aria-hidden="true"
                />
                <input
                  type="search"
                  aria-label={`Search within ${category.title}`}
                  value={searchQuery}
                  onChange={(e) => setSearchQuery(e.target.value)}
                  placeholder={`Search ${category.shortTitle.toLowerCase()}...`}
                  className="w-full pl-9 pr-8 py-2 text-sm bg-[#FAF8F5] border border-[#DFD6C7] rounded-md text-[#1B1917] placeholder:text-[#5A544E]/70 focus:outline-none focus:border-[#A68142]"
                />
                {searchQuery && (
                  <button
                    type="button"
                    aria-label="Clear search"
                    onClick={() => setSearchQuery('')}
                    className="absolute right-2.5 top-1/2 -translate-y-1/2 text-[#5A544E] hover:text-[#1B1917] cursor-pointer"
                  >
                    <X className="w-3.5 h-3.5" aria-hidden="true" />
                  </button>
                )}
              </div>

              <div className="relative flex items-center">
                <ArrowUpDown
                  className="w-3.5 h-3.5 text-[#5A544E] absolute left-3 pointer-events-none"
                  aria-hidden="true"
                />
                <select
                  aria-label={`Sort ${category.title}`}
                  value={sortBy}
                  onChange={(e) => setSortBy(e.target.value as ProductSortOption)}
                  className="w-full sm:w-auto pl-8 pr-4 py-2 text-xs font-medium bg-[#FAF8F5] border border-[#DFD6C7] rounded-md text-[#1B1917] focus:outline-none focus:border-[#A68142] cursor-pointer"
                >
                  <option value="featured">Sort: Featured</option>
                  <option value="name-asc">Sort: Name (A–Z)</option>
                  <option value="name-desc">Sort: Name (Z–A)</option>
                </select>
              </div>
            </div>
          </div>
        </div>
      </section>

      {/* Product Grid */}
      <section className="py-12 lg:py-16">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          {hasDemoEntries && (
            <div className="mb-6 p-4 rounded-lg bg-[#F2EDE4] border border-[#DFD6C7] flex flex-col sm:flex-row sm:items-center justify-between gap-3 text-xs text-[#5A544E]">
              <span>
                <strong className="text-[#1B1917]">Demonstration Catalogue Notice:</strong>{' '}
                Entries marked <em>Sample Demonstration</em> represent showroom categories
                and can be replaced with live inventory in{' '}
                <code className="text-[#1B1917]">src/data/catalogue.ts</code>.
              </span>
              <button
                type="button"
                onClick={() => setHideDemoItems(true)}
                className="text-xs font-semibold text-[#1B1917] underline hover:text-[#7D5D26] whitespace-nowrap cursor-pointer self-start sm:self-auto"
              >
                Hide demonstration items
              </button>
            </div>
          )}

          <div className="flex flex-wrap items-center justify-between gap-3 mb-6 text-xs text-[#5A544E]">
            <p className="tabular-nums">
              Showing {filteredProducts.length}{' '}
              {filteredProducts.length === 1 ? 'entry' : 'entries'} in{' '}
              <span className="font-semibold text-[#1B1917]">
                {selectedSubcategory === 'All' ? category.title : selectedSubcategory}
              </span>
            </p>

            {hasActiveFilters && (
              <button
                type="button"
                onClick={resetAllFilters}
                className="text-xs font-semibold text-[#7D5D26] hover:underline cursor-pointer"
              >
                Clear all filters
              </button>
            )}
          </div>

          {filteredProducts.length > 0 ? (
            <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-7">
              {filteredProducts.map((product) => (
                <ProductCard
                  key={product.id}
                  product={product}
                  config={config}
                  onViewDetails={onSelectProduct}
                />
              ))}
            </div>
          ) : (
            <div className="py-16 px-6 text-center bg-white border border-[#DFD6C7] rounded-lg">
              <h2 className="font-display text-2xl font-semibold text-[#1B1917]">
                {hideDemoItems
                  ? 'Live inventory entries not yet added'
                  : 'No matching items found'}
              </h2>
              <p className="mt-2 text-sm text-[#5A544E] max-w-md mx-auto">
                {hideDemoItems
                  ? `No non-demonstration items have been added to ${category.title} yet. Show demonstration entries or enquire on WhatsApp for current in-store stock.`
                  : `No catalogue entries matched your current filter or search term. Reset filters to view all ${category.title.toLowerCase()} entries.`}
              </p>
              <button
                type="button"
                onClick={resetAllFilters}
                className="mt-5 px-5 py-2.5 text-xs font-semibold bg-[#1B1917] text-[#FAF8F5] rounded-md hover:bg-[#322E2A] cursor-pointer"
              >
                Reset Filters
              </button>
            </div>
          )}
        </div>
      </section>

      {/* Cross-Category Navigation */}
      <section className="py-12 border-t border-[#DFD6C7] bg-[#F2EDE4]/45">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <h2 className="font-display text-2xl font-semibold text-[#1B1917] mb-6">
            Explore Other Departments
          </h2>
          <div className="grid grid-cols-2 sm:grid-cols-3 lg:grid-cols-6 gap-4">
            {otherCategories.map((other) => (
              <a
                key={other.id}
                href={other.route}
                onClick={(e) => {
                  e.preventDefault();
                  onNavigate(other.route);
                }}
                className="p-4 bg-white border border-[#DFD6C7] rounded-lg hover:border-[#A68142] transition-colors"
              >
                <p className="font-display text-base font-semibold text-[#1B1917]">
                  {other.shortTitle}
                </p>
                <p className="mt-1 text-xs text-[#5A544E] line-clamp-2">
                  {other.tagline}
                </p>
              </a>
            ))}
          </div>
        </div>
      </section>
    </div>
  );
}
import { useState } from 'react';
import {
  Phone,
  MessageCircle,
  MapPin,
  Clock,
  Mail,
  SlidersHorizontal,
  ExternalLink,
  Loader2,
  CheckCircle2,
  AlertCircle,
} from 'lucide-react';
import { CATEGORIES } from '../data/catalogue';
import {
  formatFullAddress,
  hasConfiguredEmail,
  hasConfiguredHours,
  type BusinessConfig,
} from '../config/businessConfig';
import { validateEnquiryForm } from '../utils/catalogueLogic';
import {
  buildGoogleMapsEmbedUrl,
  buildGoogleMapsUrl,
  buildWhatsAppGeneralUrl,
} from '../utils/whatsapp';

interface ContactPageProps {
  config: BusinessConfig;
  onOpenSettings: () => void;
}

export function ContactPage({ config, onOpenSettings }: ContactPageProps) {
  const [customerName, setCustomerName] = useState('');
  const [selectedDepartment, setSelectedDepartment] = useState("Men's Collection");
  const [customNote, setCustomNote] = useState('');
  const [formError, setFormError] = useState<string | null>(null);
  const [isSubmitting, setIsSubmitting] = useState(false);
  const [submittedUrl, setSubmittedUrl] = useState<string | null>(null);
  const [submittedPreview, setSubmittedPreview] = useState<string>('');
  const [popupWarning, setPopupWarning] = useState(false);

  const fullAddress = formatFullAddress(config);
  const mapsUrl = buildGoogleMapsUrl(config.mapQuery || fullAddress);
  const mapsEmbedUrl = buildGoogleMapsEmbedUrl(config.mapQuery || fullAddress);
  const showEmail = hasConfiguredEmail(config.email);
  const showHours = hasConfiguredHours(config);

  const handleEnquirySubmit = (e: React.FormEvent) => {
    e.preventDefault();
    setFormError(null);
    setPopupWarning(false);
    setSubmittedUrl(null);

    const validationError = validateEnquiryForm({
      customerName,
      department: selectedDepartment,
      message: customNote,
    });
    if (validationError) {
      setFormError(validationError);
      return;
    }

    const composedMessage = `Hello, my name is ${customerName.trim()}. I am enquiring about ${selectedDepartment} at ${config.businessName}: ${customNote.trim()}`;
    const targetUrl = buildWhatsAppGeneralUrl(
      config.whatsappNumber,
      config.businessName,
      composedMessage
    );

    setIsSubmitting(true);
    window.setTimeout(() => {
      setIsSubmitting(false);
      setSubmittedUrl(targetUrl);
      setSubmittedPreview(composedMessage);
      try {
        const opened = window.open(targetUrl, '_blank', 'noopener,noreferrer');
        if (!opened) {
          setPopupWarning(true);
        }
      } catch {
        setPopupWarning(true);
      }
    }, 350);
  };

  return (
    <div className="bg-[#FAF8F5]">
      <section className="border-b border-[#DFD6C7] bg-[#F2EDE4]/55">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-12 lg:py-16">
          <div className="flex flex-col md:flex-row md:items-end justify-between gap-6">
            <div>
              <p className="text-xs uppercase tracking-widest text-[#7D5D26] font-semibold">
                Showroom Support &amp; Directions
              </p>
              <h1 className="mt-2 font-display text-3xl sm:text-5xl font-semibold text-[#1B1917]">
                Contact Us
              </h1>
              <p className="mt-3 text-base text-[#5A544E] max-w-2xl">
                Reach {config.businessName} by phone, WhatsApp, or visit our showroom in person.
                Showroom details can be updated anytime without editing website code.
              </p>
            </div>

            <button
              type="button"
              onClick={onOpenSettings}
              className="inline-flex items-center gap-2 px-4 py-3 text-xs font-semibold bg-[#1B1917] text-[#FAF8F5] rounded-md hover:bg-[#322E2A] transition-colors cursor-pointer self-start md:self-auto shrink-0"
            >
              <SlidersHorizontal className="w-4 h-4 text-[#D4AF6A]" aria-hidden="true" />
              <span>Adjust Contact, WhatsApp &amp; Address</span>
            </button>
          </div>
        </div>
      </section>

      <section className="py-12 lg:py-16">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 space-y-10">
          <div className="grid grid-cols-1 lg:grid-cols-12 gap-8">
            {/* Showroom Details Card */}
            <div className="lg:col-span-6 bg-white border border-[#DFD6C7] rounded-lg p-6 sm:p-8 space-y-6">
              <h2 className="font-display text-2xl font-semibold text-[#1B1917]">
                Showroom Information
              </h2>

              <div className="space-y-5">
                <div className="flex items-start gap-3.5">
                  <Phone className="w-5 h-5 text-[#7D5D26] shrink-0 mt-0.5" aria-hidden="true" />
                  <div>
                    <p className="text-xs uppercase tracking-wider text-[#5A544E] font-medium">
                      Contact Number
                    </p>
                    <a
                      href={`tel:${config.phoneHref}`}
                      className="mt-1 block text-base font-semibold text-[#1B1917] hover:text-[#7D5D26] tabular-nums"
                    >
                      {config.phoneDisplay}
                    </a>
                  </div>
                </div>

                <div className="flex items-start gap-3.5">
                  <MessageCircle
                    className="w-5 h-5 text-[#7D5D26] shrink-0 mt-0.5"
                    aria-hidden="true"
                  />
                  <div>
                    <p className="text-xs uppercase tracking-wider text-[#5A544E] font-medium">
                      WhatsApp Number
                    </p>
                    <p className="mt-1 text-base font-semibold text-[#1B1917] tabular-nums">
                      +{config.whatsappNumber}
                    </p>
                  </div>
                </div>

                {showEmail && (
                  <div className="flex items-start gap-3.5">
                    <Mail className="w-5 h-5 text-[#7D5D26] shrink-0 mt-0.5" aria-hidden="true" />
                    <div>
                      <p className="text-xs uppercase tracking-wider text-[#5A544E] font-medium">
                        Email
                      </p>
                      <a
                        href={`mailto:${config.email}`}
                        className="mt-1 block text-sm font-medium text-[#1B1917] hover:text-[#7D5D26] break-all"
                      >
                        {config.email}
                      </a>
                    </div>
                  </div>
                )}

                <div className="flex items-start gap-3.5">
                  <MapPin className="w-5 h-5 text-[#7D5D26] shrink-0 mt-0.5" aria-hidden="true" />
                  <div>
                    <p className="text-xs uppercase tracking-wider text-[#5A544E] font-medium">
                      Showroom Address
                    </p>
                    <p className="mt-1 text-sm text-[#1B1917] leading-relaxed">{fullAddress}</p>
                    <a
                      href={mapsUrl}
                      target="_blank"
                      rel="noopener noreferrer"
                      className="mt-1.5 inline-flex items-center gap-1 text-xs font-semibold text-[#7D5D26] hover:underline"
                    >
                      <span>Open in Google Maps</span>
                      <ExternalLink className="w-3 h-3" aria-hidden="true" />
                    </a>
                  </div>
                </div>

                <div className="flex items-start gap-3.5">
                  <Clock className="w-5 h-5 text-[#7D5D26] shrink-0 mt-0.5" aria-hidden="true" />
                  <div>
                    <p className="text-xs uppercase tracking-wider text-[#5A544E] font-medium">
                      Business Hours
                    </p>
                    {showHours ? (
                      <>
                        {config.businessHours.weekdays && (
                          <p className="mt-1 text-sm text-[#1B1917]">
                            {config.businessHours.weekdays}
                          </p>
                        )}
                        {config.businessHours.sunday && (
                          <p className="mt-0.5 text-sm text-[#5A544E]">
                            {config.businessHours.sunday}
                          </p>
                        )}
                      </>
                    ) : (
                      <p className="mt-1 text-sm text-[#5A544E]">
                        Opening hours not yet listed — call or enquire on WhatsApp, or set
                        hours via <strong>Adjust Contact, WhatsApp &amp; Address</strong>.
                      </p>
                    )}
                  </div>
                </div>
              </div>
            </div>

            {/* Validated WhatsApp Enquiry Form with Loading & Error States */}
            <form
              onSubmit={handleEnquirySubmit}
              noValidate
              className="lg:col-span-6 bg-white border border-[#DFD6C7] rounded-lg p-6 sm:p-8 flex flex-col justify-between"
            >
              <div>
                <h2 className="font-display text-2xl font-semibold text-[#1B1917]">
                  Send a WhatsApp Enquiry
                </h2>
                <p className="mt-2 text-sm text-[#5A544E]">
                  Enter your name, choose a department, and describe what you are looking for
                  to prepare a direct WhatsApp message to +{config.whatsappNumber}.
                </p>

                {formError && (
                  <div
                    role="alert"
                    className="mt-4 p-3.5 rounded-md bg-red-50 border border-red-200 flex items-start gap-2.5 text-xs text-red-800"
                  >
                    <AlertCircle className="w-4 h-4 shrink-0 mt-0.5" aria-hidden="true" />
                    <span>{formError}</span>
                  </div>
                )}

                {submittedUrl && (
                  <div
                    role="status"
                    className="mt-4 p-4 rounded-md bg-[#F2EDE4] border border-[#DFD6C7] space-y-2 text-xs text-[#1B1917]"
                  >
                    <div className="flex items-start gap-2 font-semibold">
                      <CheckCircle2
                        className="w-4 h-4 text-[#7D5D26] shrink-0 mt-0.5"
                        aria-hidden="true"
                      />
                      <span>
                        {popupWarning
                          ? 'Your enquiry is ready! Your browser blocked the automatic tab — click below to open WhatsApp.'
                          : 'WhatsApp enquiry prepared for your showroom desk.'}
                      </span>
                    </div>
                    <p className="text-[#5A544E] italic">“{submittedPreview}”</p>
                    <a
                      href={submittedUrl}
                      target="_blank"
                      rel="noopener noreferrer"
                      className="inline-flex items-center gap-1.5 font-semibold text-[#7D5D26] hover:underline"
                    >
                      <span>Open WhatsApp Enquiry Link</span>
                      <ExternalLink className="w-3.5 h-3.5" aria-hidden="true" />
                    </a>
                  </div>
                )}

                <div className="mt-6 space-y-4">
                  <div>
                    <label
                      htmlFor="contact-name"
                      className="block text-xs font-semibold text-[#1B1917] mb-1.5"
                    >
                      Your Name <span className="text-[#7D5D26]">*</span>
                    </label>
                    <input
                      id="contact-name"
                      type="text"
                      required
                      value={customerName}
                      onChange={(e) => {
                        setCustomerName(e.target.value);
                        if (formError) setFormError(null);
                      }}
                      placeholder="Enter your name"
                      className="w-full px-3.5 py-2.5 text-sm bg-[#FAF8F5] border border-[#DFD6C7] rounded-md text-[#1B1917] focus:outline-none focus:border-[#A68142]"
                    />
                  </div>

                  <div>
                    <label
                      htmlFor="contact-dept"
                      className="block text-xs font-semibold text-[#1B1917] mb-1.5"
                    >
                      Department of Interest
                    </label>
                    <select
                      id="contact-dept"
                      value={selectedDepartment}
                      onChange={(e) => setSelectedDepartment(e.target.value)}
                      className="w-full px-3.5 py-2.5 text-sm bg-[#FAF8F5] border border-[#DFD6C7] rounded-md text-[#1B1917] focus:outline-none focus:border-[#A68142]"
                    >
                      {CATEGORIES.map((cat) => (
                        <option key={cat.id} value={cat.title}>
                          {cat.title}
                        </option>
                      ))}
                      <option value="General Showroom Enquiry">General Showroom Enquiry</option>
                    </select>
                  </div>

                  <div>
                    <label
                      htmlFor="contact-note"
                      className="block text-xs font-semibold text-[#1B1917] mb-1.5"
                    >
                      Your Enquiry <span className="text-[#7D5D26]">*</span>
                    </label>
                    <textarea
                      id="contact-note"
                      rows={3}
                      required
                      value={customNote}
                      onChange={(e) => {
                        setCustomNote(e.target.value);
                        if (formError) setFormError(null);
                      }}
                      placeholder="Ask about specific brands, sizes, furniture dimensions, electronics model numbers, or availability..."
                      className="w-full px-3.5 py-2.5 text-sm bg-[#FAF8F5] border border-[#DFD6C7] rounded-md text-[#1B1917] focus:outline-none focus:border-[#A68142]"
                    />
                  </div>
                </div>
              </div>

              <div className="mt-6 pt-5 border-t border-[#EFECE6]">
                <button
                  type="submit"
                  disabled={isSubmitting}
                  className="w-full inline-flex items-center justify-center gap-2 px-6 py-3.5 text-sm font-semibold bg-[#1B1917] text-[#FAF8F5] rounded-md hover:bg-[#322E2A] disabled:opacity-70 transition-colors cursor-pointer"
                >
                  {isSubmitting ? (
                    <>
                      <Loader2 className="w-4 h-4 animate-spin text-[#D4AF6A]" aria-hidden="true" />
                      <span>Preparing WhatsApp Enquiry...</span>
                    </>
                  ) : (
                    <>
                      <MessageCircle className="w-4 h-4 text-[#D4AF6A]" aria-hidden="true" />
                      <span>Send Enquiry on WhatsApp</span>
                    </>
                  )}
                </button>
              </div>
            </form>
          </div>

          {/* Embedded Map */}
          <div className="bg-[#F2EDE4] border border-[#DFD6C7] rounded-lg overflow-hidden">
            <iframe
              title={`${config.businessName} Google Map`}
              src={mapsEmbedUrl}
              loading="lazy"
              referrerPolicy="no-referrer-when-downgrade"
              className="w-full h-[360px] border-0"
            />
          </div>
        </div>
      </section>
    </div>
  );
}
