---
title: Strona główna
mobile_menu_title: "Strona główna"
---
{{< slogan get_started="ZACZNIJ TUTAJ" docs="Dokumentacja" notes="Zmiany" lang="en" >}}
Zig to język programowania oraz zestaw narzędzi do tworzenia **wydajnego** i **stabilego** oprogramownia **wielokrotnego użytku**.
{{< /slogan >}}

{{< flexrow class="container" style="padding: 20px 0; justify-content: space-between;" >}}
{{% div class="features" %}}

# ⚡ Prosty język
Skup się na debugowaniu swoich aplikacji, a nie wiedzy o języku.

- Brak ukrytego przepływu kontroli.
- Brak ukrytych alokacji pamięci.
- Brak preprocesora oraz makr.

# ⚡ Comptime
Świeże podejście do metaprogramowania, oparte na ewaluacji kodu w czasie jego kompilacji.

- Każda funkcja może być wykonana podczas kompilacji.
- Manipuluj typami jak zwykłymi wartościami, bez żadnych kosztów po kompilacji.
- Comptime zawsze naśladuje docelową architekturę.

# ⚡ Utrzymuj kod z językiem Zig
Przyrostowo polepszaj swoją bazę kodową uzywającą C/C++/Zig.

- Użyj kompilatora Zig jako niezależnego kompilatora C/C++ ze wsparciem wielu architektur.
- Użyj `zig build` aby utworzyć spójne środowisko programistyczne między wszystkimi platformami.
- Dodaj kod Zig do projektów napisanych w C/C++; miedzyjęzykowa optymalizacja w czasie linkowania (LTO) jest włączona domyślnie.

{{% flexrow style="justify-content:center;" %}}
{{% div %}}
<h1>
    <a href="learn/overview/" class="button" style="display: inline;">Głębszy przegląd</a>
</h1>
{{% /div %}}
{{% div  style="margin-left: 5px;" %}}
<h1>
    <a href="learn/samples/" class="button" style="display: inline;">Więcej przykładów</a>
</h1>
{{% /div %}}
{{% /flexrow %}}
{{% /div %}}
{{< div class="codesample" >}}

{{% zigdoctest "assets/zig-code/index.zig" %}}

{{< /div >}}
{{< /flexrow >}}


{{% div class="alt-background" %}}
{{% div class="container"  style="display:flex;flex-direction:column;justify-content:center;text-align:center; padding: 20px 0;" title="Społeczność" %}}

{{< flexrow class="container" style="justify-content: center;" >}}
{{% div style="width:25%" %}}
<img src="/ziggy.svg" style="max-height: 200px">
{{% /div %}}

{{% div class="community-message" %}}
# Społeczność Zig jest zdecentralizowana
Każdy może otworzyć swoje własne miejsca dla spotkań społeczności.
Nie istnieje koncept miejsc "oficjalnych" i "nieoficjalnych", aczkolwiek każda platforma ma swoich własnych moderatorów oraz własne zasady.

<div style="">
<h1>
	<a href="https://github.com/ziglang/zig/wiki/Community" class="button" style="display: inline;">Znajdź wszystkie społeczności (ang.)</a>
</h1>
</div>
{{% /div %}}
{{< /flexrow >}}
<div style="height: 50px;"></div>

{{< flexrow class="container" style="justify-content: center;" >}}
{{% div class="main-development-message" %}}
# Główny rozwój
Repozytorium języka Zig można znaleźć na stronie [https://github.com/ziglang/zig](https://github.com/ziglang/zig), gdzie można zgłaszać problemy oraz dyskutować nad propozycjami rozwoju języka.
Kontrybutorzy muszą przestrzegać naszego [Kodeksu postępowania (ang. Code of Conduct)](https://github.com/ziglang/zig/blob/master/CODE_OF_CONDUCT.md).
{{% /div %}}
{{% div style="width:40%" %}}
<img src="/zero.svg" style="max-height: 200px">
{{% /div %}}
{{< /flexrow >}}
{{% /div %}}
{{% /div %}}


{{% div class="container" style="display:flex;flex-direction:column;justify-content:center;text-align:center; padding: 20px 0;" title="Fundacja Oprogramowania Zig" %}}
## ZSF to korporacja non-profit.

Zig Software Foundation (pol. Fundacja Oprogramowania Zig) to korporacja non-profit założona w 2020 roku przez Andrew Kelley'ego, twórcę języka Zig, z celem wspierania rozwoju projektu. Aktualnie ZSF jest w stanie oferować płatną pracę po konkurencyjnych stawkach dla małej ilości głównych kontrybutorów. Mamy nadzieję, że z czasem będziemy mogli poszerzyć tą ofertę.

Fundacja Oprogramowania Zig jest opłacana z darowizn.

<h1>
	<a href="zsf/" class="button" style="display:inline;">Dowiedz się więcej</a>
</h1>
{{% /div %}}


{{< div class="alt-background" style="padding: 20px 0;">}}
{{% div class="container" title="Sponsorzy" %}}
# Sponsorzy korporacyjni
Poniżej wymienione firmy zapewniają bezpośrednie wsparcie finansowe dla Fundacji Oprogramowania Zig.

{{% sponsor-logos "monetary" %}}
 <a href="https://pex.com" rel="noopener nofollow" target="_blank"><picture>
   <picture>
     <source srcset="/pex-white.svg" media="(prefers-color-scheme: dark)">
     <img src="/pex-dark.svg">
   </picture>
 </a>
{{% /sponsor-logos %}}

# Sponsorzy w serwisie GitHub
Dzięki wszystkim, którzy [sponsorują język Zig](zsf/), ten projekt może odpowiadać społeczności, a nie korporacyjnym akcjonariuszom. W szczególności, ci mili ludzie sponsorują Zig za $200 miesięcznie lub więcej:

{{< ghsponsors >}}

Powyższa sekcja jest aktualizowana na początku każdego miesiąca.
{{% /div %}}
{{< /div >}}
























