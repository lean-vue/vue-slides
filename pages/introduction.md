
# Einführung: Was ist Vue?

<div class="text-2xl mt-12 px-8">
Vue (ausgesprochen /vjuː/, wie *view* im Englischen) ist ein JavaScript Framework zur
Erstellung von Benutzeroberflächen.
</div>
<div class="text-2xl mt-8 px-8">
Es basiert auf den Standards HTML, CSS und JavaScript und bietet ein deklaratives
und Komponenten-orientiertes Programmier-Model zur effizienten UI-Entwicklung
- von einfach bis komplex.
</div>

---

# Einführung: Beispiel

```vue
<script>
export default {
  props: ['count'],
  data: function () { return {counter: this.count ?? 0 } }
}
</script>

<template>
  <div class="ml-4">
    <button class="border rounded px-4 py-2 hover:bg-gray-100 dark:hover:bg-gray-800" @click="counter++">
      Count is: {{ counter }}
    </button>
  </div>
</template>
```

Ergebnis:

<Counter :count="17" />

---

# Einführung: Beispiel

<div><p>
Das vorherige Beispiel demonstriert bereits zwei Kern-Konzepte von Vue:
</p></div>

- **Deklaratives Rendern**: Vue erweitert Standard-HTML um eine Template-Syntax, die uns erlaubt
deklarativ die HTML-Ausgabe zu beschreiben - basierend auf Daten (einem *State*) beschrieben in JavaScript.
- **Reaktivität**: Vue überwacht den State auf Änderungen und passt die DOM-Ausgabe entsprechend an.
- **Single-File-Components**: HTML, Styles und der Komponenten-Code sind in einer Datei.

---

# Einführung: The Progressive Framework

<div><p>
Vue ist sowohl Framework als auch Ecosystem mit Unterstützung für die wichtigsten Anwendungsszenarien
in der Web-Frontendentwicklung. Es ist dabei derart gestaltet, dass der Einsatz von Vue flexibel mit den
Anforderungen gesteigert werden kann.
</p></div>

Mögliche Varianten des Einsatzes von Vue:

- Enhancing static HTML without a build step
- Embedding as Web Components on any page
- Single-Page Application (SPA)
- Fullstack / Server-Side-Rendering (SSR)
- JAMStack / Static-Site-Generation (SSG)

---

# Einführung: Single-File Components

<div><p>
In den meisten Vue-Projekten mit Build-Tool Unterstützung werden die Komponenten in einem HTML-ähnlichen
Format geschrieben - genannt **Single-File Component** (auch bekannt als `*.vue` Dateien, abgekürzt mit **SFC**).
Eine VUE SFC kapselt die Komponenten-Logik (JavaScript), das Template (HTML), and die Styles (CSS) in
einer einzelnen Datei.
</p></div>

SFC sind ein Vue auszeichnendes Feature und der empfohlene Weg Vue Komponenten zu schreiben. Vorausgesetzt
wir setzen ein Build-Tool Setup im Projekt ein!

---

# Einführung: SFC Beispiel

```vue
<script>
export default {
  data() {
    return {
      count: 0
    }
  }
}
</script>

<template>
  <button @click="count++">Count is: {{ count }}</button>
</template>

<style scoped>
button {
  font-weight: bold;
}
</style>
```

---

# Einführung: API Styles

<div><p>
Vue Komponenten können mit zwei unterschiedlichen Schnittstellen API programmiert werden:
</p></div>

- **Options API**
- **Composition API**

---

# Einführung: Options API

<div><p>
Mit der Options API definieren wir die Komponenten-Logik mit einem Objekt und Optionen. Properties dieser
Optionen werden auf der Komponenten-Instanz bereitgestellt. Der `this`-Zeiger wird umgebogen auf diese.
</p></div>

```vue
<script>
export default {
  data() {
    return {
      count: 0
    }
  },
  methods: {
    increment() {
      this.count++
    }
  },
  mounted() {
    console.log(`The initial count is ${this.count}.`)
  }
}
</script>
```

---

# Einführung: Composition API

<div><p>
Mit der Composition API definieren wir die Komponenten-Logik mit importierten API Funktionen. In SFC wird die
Composition API typischerweise benutzt mit einem Setup-Script (&lt;script setup>).Das setup Attribut reduziert einiges
an Boilerplate Code, der durch Code-Transformationen beim Build bereitgestellt wird.
</p></div>

```vue
<script setup>
import { ref, onMounted } from 'vue';

const count = ref(0);

function increment() {
  count.value++;
}

onMounted(() => {
  console.log(`The initial count is ${count.value}.`);
});
</script>
```

---

# Einführung: Welche API?

<div><p>
Zunächst gilt, das beide API komplett gleichwertig sind. Die fundamentalen Vue-Konzepte liegen beiden zugrunde.
Sie stellen einfach zwei unterschiedliche Schnittstellen auf die Kern-API dar. Tatsächlich wurde die Options API
auf der Composition API implementiert.
</p></div>

Die Options API betont das Konzept einer *Komponenten-Instanz* (mit dem `this`-Zeiger auf diese) - was typischerweise
besser mit einem klassen-basierten mentalen Modell korreliert. Zudem ist es durchaus etwas einsteiger-freundlicher, da
einige Kern-Konzepte in der Options API elegant abstrahiert sind.

Die Composition API deklariert den reaktiven State direkt im Function-Scope und setzt diesen aus mehreren einzelnen
Funktionen zusammen. Der Code ist flexibler (free-form) und verlangt nach vertieftem Wissen über die Reaktivität in Vue.
Im Gegenzug belohnt uns diese Flexibilität mit mächtigeren Mustern bei der Organisation und Wiederverwendung von Logik.

---

# Einführung: Welche API?

- Zum Erlernen beginne mit dem Stil, der dir einfacher erscheint.

- Produktiv:

  - Nutze die Options API, wenn keine Build-Tools im Spiel sind oder Vue nur einfach zur Aufwertung von bisher
    statischem HTML benutzt wird.

  - Nutze die Composition API + Single-File Components, wenn du planst komplette Anwendungen mit Vue zu schreiben.
