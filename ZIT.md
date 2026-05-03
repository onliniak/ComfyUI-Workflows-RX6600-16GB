# Z Image Turbo - Notes - Prompty

::NOTE:: Ten styl został zablokowany w Flux2 Klein ze względów bezpieczeństwa.

Kiedyś już popełniłem największy błąd w swoim życiu i poszedłem do pracy.
Ze względu na lepiej rozwinięty mózg nie udało mi się zrozumieć tych poleceń LLM.

Teraz jako über menedżer muszę określić ile czasu (kroków) zajmie mojemu pracownikowi (ZIT)
wykonanie zadania i nadać mu realne priorytety (prompt), które ma szansę ukończyć
we wskazanym terminie. Jeśli nie zdąży to jest to tylko i wyłącznie moja wina.

## Przykładowe prompty

```
ßrumßrum是一张看起来像鳄鱼皮的沙发。

$AK47$ 是金发女，$AK56$ 是黑发女。

一个名叫 $AK56$ 的女孩躺在 ßrumßrum 的座位上，
$AK56$ 的双腿支撑在 ßrumßrum 的靠背上，
$AK56$ 的脚靠在 ßrumßrum 上方的墙上，
$AK56$ 的手垂在地板上，
同一个 ßrumßrum 上躺着一个名叫 $AK47$ 的女孩，
$AK47$ 仰躺，$AK47$ 的腿在 $AK56$ 的头上方抬起，
$AK47$ 的手沿着她的身体放置。
```

albo

```
ßrumßrum 是 một 沙发，看起来好像覆盖着鳄鱼皮, ßumßum 是 một 藤椅，距离 ßrumßrum 两米远。

$AK47$ 是一个来自北方的女人，$AK47$ 身高 152 厘米，$AK47$ 体重 30 公斤，$AK47$ 戴着一个 RGB 颜色值为 7985100 的帽子, $AK56$ 是 $AK47$ 的单卵双胞胎，$AK56$ 体重 123 公斤，$AK56$ 戴着一个 RGB 颜色值为 11065209 的鸭舌帽。

$AK47$ 坐在 ßumßum 上，$AK56$ 躺在 ßrumßrum 上。

把摄像头调到俯视图，光线处于黄金时刻。
```

i po polsku

```
Ścieżka rowerowa biegnie wzdłuż plaży, w tle widzimy morze.

Jedzie po niej rower górski.

Rowerzystą jest Koreańczyk w okularach przeciwsłonecznych, o niebieskich oprawkach i fioletowych szkłach.

Kamera jest ustawiona po skosie względem rowerzysty.
```

```
# Variables.

Young Chinese woman named $AK47$ in red Hanfu, intricate embroidery. Impeccable makeup, red floral forehead pattern. Elaborate high bun, golden phoenix headdress, red flowers, beads.

$DrewnianyBlok$ = wooden cubic block. $DrewnianyBlok$ is not visible unless $AK47$ is not visible.

# Prompt.

Divide screen at 2 equal panels. On left panel is $AK47$, on right panel $AK47$ is not visible.
```

- Z-Image-Turbo nie tylko obsługuje zmienne (dowolne słowo jakiego nie rozumie) ale też warunki (*unless* jak w Ruby).
- Komentarze oznaczamy kratką (#)

```
Zakładając, że na wprost od Ciebie znajduje się czerwony drewniany blok, po Twojej prawej stronie zielony drewniany blok, a po Twojej lewej stronie niebieski drewniany blok. Uwzględniwszy iż zielony i niebieski blok nie mogą się pojawić na jednej scenie.

Podziel ekran na 3 równe części: na lewym scena jest obrócona o 90° w lewo, na prawym scena jest obrócona o 90° w prawo, na środkowym scena jest widoczna pod kątem z dołu.
```

Odpowiedzią na zagadkę jest czerwony blok przesunięty lekko w prawo po lewej stronie
oraz zielony blok lekko przesunięty w lewo po prawej stronie. 

```
Playground on the middle of park. Behind you is waterfall.

Divide screen at 3 equal panels, left panel show camera turned by 90° to left, middle panel has volumetric fog, right panel show camera turned by 180° to right.
```

Bardzo ciekawy eksperyment, bo z ludzkiego punktu widzenia praktycznie niewykonalny.
Jeśli znajduję się w pustej przestrzeni pośrodku niczego, wiem co jest przede mną
i wiem co jest za mną ale nie ma absolutnie niczego obok mnie to skąd mam wiedzieć
jak obrócić się w bok ?

Wyszło coś takiego:
- Pośrodku mam wodospad, na dole woda tworzy coś między mgłą, a dymem jak chciałem.
- Po obu stronach mam identyczny obraz ale z detalami w różnych kolorach.

## Syntax

Zasady tego języka programowania są bardzo proste:
- Testowane na moim ulubionym LMS.
- Chiński kropek (。) oznacza MAY zgodnie z RFC2119
    - ZIT najprawdopodobniej zignoruje wszystko, co jest dalej
- Biała linia (SHIFT+ENTER) oznacza poszczególne kroki
- męski przecinek (a,b) jak i babski przecinek (a , b) oznaczają szczegóły
- W jednym kroku polecenie będzie kontynuowane tak długo, aż szczegół A
będzie się kłócił ze szczegółem B, wtedy ZIT sam zdecyduje co zostawi, a co usunie.
- Ustawienia kamery i pierwsze zdanie mają najwyższy priorytet.
- LMS jest z natury leniwy, więc mówiąc o jednej osobie na krześle, a
drugiej na sofie po prostu posadzi obie osoby na kanapie.
- Jeśli ktoś pisze o robalich okach, żabach i ptakach to nic dziwnego, że nic mu nie wychodzi.
Chińskie modele rozumieją poprawne określenia jak: kamera pod kątem z góry/dołu,
z widoku drona, płaskie uderzenie (z widoku oczu (?)), obróć scenę o 90° w lewo/prawo,
przestaw obiektyw na szerokokątny, przesuń kamerę do przodu/tyłu. Tego rodzaju rzeczy.
- ZIT rozumie polecenie "pokaż jak (będzie) wyglądało moje ciało w wieku X lat"
    - Ale podobnie jak w przypadku bliźniaka po prostu skopiuje wszystkie szczegóły z obiektu rodzica
- ZIT rozumie kolory (ComfyUI ma osobny węzeł od RGB int)
- ZIT widzi świat 3D, stąd polecenie przestaw krzesło 2 metry dalej odczyta prawidłowo (o ile zmieści się w obiektywie).
- Generowanie polskich znaków nie najlepiej mu wychodzi
- Jeśli napiszesz, że ktoś ma się odwrócić plecami ALE opiszesz szczegóły twarzy
to się nie zdziw, jak ZIT będzie próbował połączyć oba obrazy w jeden.
- Jak wpiszesz seed z perchance.org i użyjesz Eulera Simple to najprawdopodobniej
otrzymasz identyczne zdjęcie.
- Zauważ, że nie piszę chudy/gruby, wysoki/niski tylko podaję wartości fizyczne.
Możesz też opisać obwód talii, bioder i wszystkiego innego. 

Właściwie to optymalizacja kosztów LMS wygląda jakoś tak:
- Wybierz jeden, główny obiekt dekoracyjny
- Pokaż ludzi
- Dokończ szczegóły dotyczące ludzi jeśli masz wystarczająco dużo kroków

### Łączenie zmiennych

Przez przypadek powstał mi eksperyment cnpsg. 1-2 minuty na wygenerowanie
zdjęcia (512x512) i o wiele lepsze podążanie za promptem, niż w poprzedniej wersji.
Tylko nie wiem czemu myli psa i jaszczurkę.

Wariant "latent" po otrzymaniu kilku przykładowych zdjęć próbuje wygenerować
coś, co spełnia wszystkie Twoje wymagania. Obecnie przestawiony na latenty.
Tak serio to od edycji zdjęć jest Z-Image-base.

Wariant 90 po prostu łączy prompty w jeden długi i każdemu z nich nadaje
ten sam priorytet (badania blackbox, sam nie wiem co robi FluxGuidance).
Do tego może zapewniać wyższą unikalność wyników, niż KSampler.
W każdym bądź razie nie dość, że działa to jeszcze wynik podoba mi się
bardziej, niż poprzednio co można uznać za sukces. Na razie oznaczam
jako eksperymentalny tryb kreatywny.