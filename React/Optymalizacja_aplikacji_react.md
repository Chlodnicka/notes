# Optymalizacja aplikacji na Reakcie

Source: https://www.youtube.com/watch?v=1mltzNfkeoY

1. Performance measuring tools - mierzenie wydajności
   - SENTRY
   - profiler w przeglądarce
1. Component vs Pure Component
1. Memoize React Components
   - React.memo()
   - useMemo()
1. Wirtualizacja długich list - wyświetlanie tylko tego co mamy na widoku (vieweport)
1. Loadable compoenenst - "ładowalne"
   - na errorze nie wywalamy całej aplikacji tylko pojedynczy komponent
1. Optymalizacja importow
    - `import _ from "loadash"`  - 71 KB
    - `import {isArray} from "loadash"` - 71 KB
    - `import isArray from "loadash/isArray"` 1 KB (cherry picking)
    - Webpack Bundle Analyzere plugin - wizualizacja paczek (ich wielkości/ciężkości)
1. Progressive image loading
1. Włączenie kompresji gzip na serwerze