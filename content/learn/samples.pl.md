---
title: "Przykłady"
mobile_menu_title: "Przykłady"
toc: true
---

## Wykrywanie wycieków pamięci
Używając `std.heap.GeneralPurposeAllocator` możesz znaleźć podwójne zwolnienia pamięci oraz jej wycieki.

{{< zigdoctest "assets/zig-code/samples/1-memory-leak.zig" >}}


## Interoperacyjność z językiem C
Przykład importowania pliku nagłówkowego w języku C, oraz linkowanie bibliotek libc oraz raylib.

{{< zigdoctest "assets/zig-code/samples/2-c-interop.zig" >}}


## Zigg Zagg
Zig jest *zoptymalizowany* dla spotkań rekrutacyjnych (właściwie to nie).

{{< zigdoctest "assets/zig-code/samples/3-ziggzagg.zig" >}}


## Typy generyczne
W jezyku Zig typy są wartościami comptime. Do implementacji generycznych, uogólnionych algorytmów i struktur danych używamy funkcji, które zwracają typy. W poniższym przykładzie implementujemy prostą kolejkę i testujemy jej działanie.

{{< zigdoctest "assets/zig-code/samples/4-generic-type.zig" >}}


## Użycie cURL z języka Zig

{{< zigdoctest "assets/zig-code/samples/5-curl.zig" >}}
