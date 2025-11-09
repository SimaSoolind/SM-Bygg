 SM BYGG & PROJEKTLEDNING AB – Webbplatsdokumentation

Detta projekt är en responsiv webbplats byggd i HTML och CSS. Fokus har legat på **Mobile-First**, **Tillgänglighet (WCAG)** och användning av moderna CSS-layouter.


## 1. Designfilosofi och Grundläggande Kodidéer

| Kodidé | Beskrivning | Var det används (CSS) |
| :--- | :--- | :--- |
| **Mobile-First** | Alla CSS-stilar är skrivna för mobilskärmar som standard. Desktop-stilar läggs till senare med **`@media (min-width: 768px)`**. | `style.css` (Överallt) |
| **Box-Sizing** | Använder **`box-sizing: border-box;`** globalt (`*`). | Gör det enkelt att hantera bredder eftersom `padding` och `border` inte räknas med i elementets totala bredd. |
| **Semantisk HTML** | Innehållet är alltid strukturerat med taggar som `<header>`, `<nav>`, `<main>`, och `<footer>` för att ge mening åt innehållet (bra för SEO och skärmläsare). | Alla HTML-filer |
| **Tillgänglighet (A11y)** | Implementering av **"Skip Link"** och tydlig **`outline`** vid fokus på länkar (`a:focus`). | `style.css` (Sektion 13) |
| **Flexbox & Grid** | Används för komplexa layouter som kort och text/bild-block (se detaljer nedan). | `style.css` (Sektion 5, 10, 12) |

---

## 2. Global HTML-struktur (Svar på "Varje sidas struktur")

Alla sidor (index, about, services, projekt) delar samma grundläggande struktur:

### A. Headern (`<header>`)
* **Logo:** Alltid högst upp.
* **"Skip Link":** En länk **`a href="#main-content" class="skip-link"`** ligger högst upp i HTML:en. Den är dold som standard men visas när användaren trycker på **Tab** (WCAG-krav).
* **Mobilmeny:** Menyn är byggd med **`<details>`** och **`<summary>`**. Detta är en ren HTML-lösning som tillåter att menyn fälls ut utan JavaScript.
    * **Tillgänglighet (A11y):** Navigeringen använder **`aria-label="Mobil Huvudmeny"`** för skärmläsare.

### B. Huvudinnehållet (`<main>`)
* Har alltid **`id="main-content"`**. Detta är målet för "Skip Link", vilket låter tangentbordsanvändare hoppa direkt förbi navigeringen.
* Innehåller alla unika sektioner, som t.ex. Värderingar, Tjänster eller Referenser.

### C. Sidfoten (`<footer>`)
* Enkel struktur med kontaktinformation och copyright.

---

## 3. Sid- och Layout-specifika Kodidéer

Dessa idéer förklarar hur de visuella elementen byggs med CSS-layouter:

### A. Startsidan (`index.html`)
| Sektion | Layoutverktyg | Kodidé/Syfte |
| :--- | :--- | :--- |
| **Värderingar** | **CSS Grid** (`display: grid;`) | Det Skapar en dynamisk **2x2-layout** på desktop, men staplas automatiskt i en kolumn på mobil Vilket är perfekt för en samling rutor. 
| **Tjänstekort** | **Flexbox** (`display: flex; flex-wrap: wrap;`) | Används för att visa korten sida vid sida. **`flex-wrap`** säkerställer att korten flyter ner på en ny rad när skärmen blir för smal (responsivt). |

### B. Tjänster (`services.html`)
| Sektion | Layoutverktyg | Kodidé/Syfte |
| :--- | :--- | :--- |
| **Tjänstelista** | **Flexbox** | Listan (`ul`) använder Flexbox för att centrera listpunkterna på mobil och fästa dem till vänster på desktop (`@media (min-width: 768px)`). |
| **Detaljblock** | **Flexbox** (`flex-direction: column;` på mobil, `row;` på desktop) | Används för att skapa block med Bild och Text. Klassen **`.layout-reverse`** används på vartannat block för att växla ordningen mellan *Bild-Text* och *Text-Bild* utan att ändra HTML:en (endast CSS-ändring via `flex-direction: row-reverse;`). |

### C. Om Oss (`about.html`)
| Sektion | Layoutverktyg | Kodidé/Syfte |
| :--- | :--- | :--- |
| **Team/Mission** | **Flexbox** | Sektionen är uppdelad i 50/50 block på desktop. Bild och Text staplas på mobil (`column`) och läggs sida vid sida på desktop (`row`). |

### D. Referenser (`projekt.html`)
| Sektion | Layoutverktyg | Kodidé/Syfte |
| :--- | :--- | :--- |
| **Referenskort** | **Flexbox** (`flex-wrap: wrap;`) | Varje projekt visas som ett kort med en flexibel bredd (**`flex-basis: 300px;`**). Detta gör att så många kort som möjligt får plats på en rad innan de flödar ner till nästa. |