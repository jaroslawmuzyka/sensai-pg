# Struktura projektu frontendowego

Projekt generowany przez platformy [bolt.new](http://bolt.new) czy lovable.dev jest oparty na Vite + TypeScript, ze zintegrowanym Tailwind CSS i PostCSS oraz ESLint do lintowania. Jego struktura:

![image](image%209.png)

*   **node_modules** – folder z wszystkimi paczkami (zainstalowanymi przez npm/yarn).
*   **src/** – kod źródłowy aplikacji.
*   **index.html** – główny HTML, w którym Vite “wstrzykuje” bundlowane skrypty.
*   **package.json** & **package-lock.json** – deklaracja zależności i skryptów.
*   **vite.config.ts** – konfiguracja bundlera Vite.
*   **tsconfig.json**, **tsconfig.app.json**, **tsconfig.node.json** – ustawienia kompilatora TypeScript dla różnych części projektu.
*   **tailwind.config.js** & **postcss.config.js** – konfiguracja frameworka CSS.
*   **.eslintrc.cjs** – konfiguracja lintera ESLint.
