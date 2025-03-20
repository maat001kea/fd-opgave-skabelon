# Opgaveskabelon til Frontend Design tema på Frontend-valgfaget

Se opgavebeskrivelsen på Fronter.

## Medfølgende API

Der medfølger en simpel API, som du kan bruge til at hente data til din opgave. Det er ikke et krav til opgaven, men det kan gøre det nemmere og hurtigere at få tekst og billeder ind i dit projekt.

Dokumentationen til API'et finder du på: [https://frontend-design-theme.netlify.app/](https://frontend-design-theme.netlify.app/).

Her er et eksempel på, hvordan du kan hente data fra API'et:

```astro
const employeesData = await fetch(
  "https://frontend-design-theme.netlify.app/api/employees"
).then((response) => response.json());

console.log(employeesData);
```

Anvendte teknologier
Astro.js – Bruges til at bygge komponentbaserede sider med hurtig rendering.
HTML5 – Strukturerer alt indhold på siderne.
CSS3 (Flexbox & Grid) – Bruges til layout og styling af komponenterne.
SVG-ikoner – Bruges til sociale medieikoner og UI-elementer.
Astro Props & Dynamic Data – Bruger dynamisk dataindlæsning til at generere teamsider.

📂 Projektstruktur
scss
Kopiér
Rediger

📦 my-project
├── 📁 public
│ ├── 📁 images (Indeholder statiske billeder)
│ ├── 📁 icons (Indeholder SVG-ikoner)
├── 📁 src
│ ├── 📁 components
│ │ ├── AboutTeam.astro (Komponent for team-sektionen)
│ │ ├── FAQ.astro (Dynamisk FAQ-sektion)
│ ├── 📁 pages
│ │ ├── index.astro (Hjemmesiden)
│ │ ├── about.astro (Om os-side)
│ ├── 📁 styles
│ │ ├── global.css (Globale CSS-styles)
│ │ ├── team.css (Specifik styling for team-sektionen)
│ │ ├── faq.css (Styling for FAQ-sektionen)
├── 📜 teamData.js (Indeholder dynamiske data om teammedlemmer)
└── 📜 README.md (Denne fil)
🎯 Refleksion over anvendte koder
1️⃣ Dynamisk Datahåndtering med Astro Props
Team-sektionens komponent bruger Astro Props til at loope igennem data fra teamData.js og generere teammedlemmer dynamisk.
En funktion getImageUrl() håndterer fejlhåndtering af billeder, så et placeholder-billede bruges, hvis intet billede er tilgængeligt.
Udfordringer:

Der opstod en fejl, hvor teamData var undefined. Dette blev løst ved at sikre, at data blev korrekt importeret i komponenten.
astro
Kopiér
Rediger

---

const { teamData } = Astro.props;

const getImageUrl = (image) => {
return image ? image : "https://via.placeholder.com/250x250.webp?text=No+Image";
};

---

2️⃣ FAQ-sektion med kun HTML & CSS (Ingen JavaScript)
Bruger <details> og <summary>-elementer til at lave en FAQ uden JavaScript.
Problem: Når én FAQ åbnes, skulle den tidligere lukkes.
Løsning: Brug af radio buttons med CSS for at sikre, at kun én kan være åben ad gangen.
html
Kopiér
Rediger

<div class="faq-item">
  <input type="radio" id="faq1" name="faq-group">
  <label for="faq1">What happens when I apply?</label>
  <div class="faq-content">Your application will be reviewed within 3-5 business days.</div>
</div>

Refleksion:

Det var en udfordring at få det til at fungere uden JavaScript, men radio-buttons løste problemet elegant.
3️⃣ Styling & Layout
Flexbox og Grid blev brugt til at skabe en responsiv struktur for både team-sektionen og FAQ-sektionen.
Ikon-placering var en udfordring, da nogle SVG-ikoner ikke viste sig korrekt. Dette blev løst ved at sikre, at de blev dynamisk indsat med set:html.
astro
Kopiér
Rediger

<div class="social-icons">
  {member.social_links.map((social) => (
    <a href={social.url} target="_blank" class="social-link">
      <span class="icon" set:html={social.icon} />
    </a>
  ))}
</div>

✅ Hvad jeg har lært
Astro Props & Dynamisk Data – Brug af Astro til at håndtere JSON-data og vise indhold dynamisk.
CSS Tricks – F.eks. brug af radio buttons til at lave en interaktiv FAQ-sektion uden JS.
Billedhåndtering – Brug af public/ korrekt, så billeder vises som de skal.
Responsivt Design – Brug af grid-template-columns til at tilpasse layout på forskellige skærmstørrelser.
📌 Forbedringer til fremtiden
Tilføje Astro API-fetching i stedet for statisk JSON for at hente data dynamisk.
Implementere Dark Mode med CSS prefers-color-scheme.
Forbedre tilgængelighed (A11Y) ved at tilføje bedre ARIA-attributter.

💡 Konklusion
Dette projekt har givet en dybere forståelse for Astro, HTML & CSS og hvordan man kan bygge en dynamisk, interaktiv hjemmeside uden brug af JavaScript. 🚀
