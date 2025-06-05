[![[d5014260581b55e554178704c68ad087_MD5.png]]

Mieliśmy okazję przekonać się o możliwościach generatywnego AI w zakresie przetwarzania tekstu i audio, a także o zdolności do interpretowania obrazu. Teraz zobaczymy jakie opcje mamy w kontekście manipulacji i generowania nowych grafik oraz zdjęć.

Projektowanie kreacji graficznych i praca ze zdjęciami do tej pory nie kojarzyły się bezpośrednio z programowaniem, z wyjątkiem rozwoju narzędzi dla tej branży czy budowania zaawansowanych interakcji z HTML Canvas i WebGL. Wydaje się zatem, że w dobie generatywnego AI, to raczej osoby zajmujące się projektowaniem, czy tworzeniem ilustracji, powinny być zainteresowane narzędziami takimi jak [Midjourney](tools/Midjourney.md) czy [Stable Diffusion](glossary/Stable%20Diffusion.md). Okazuje się jednak, że nie do końca. 

Przykładem może być narzędzie [picthing](https://pic.ping.gg/), pozwalające na skuteczne usuwanie tła ze zdjęć, zbudowane przez twórcę kanału `Theo — t3.gg`. Choć samo usuwanie tła nie jest czymś nowym, tutaj mówimy o znacznym wzroście jakości. Przede wszystkim jednak, projekt ten jest przykładem, jak generatywne AI może być wykorzystane do budowania użytecznych produktów.

![[0d5ccbf9935bfe0209bcc5698ae8d4a7_MD5.png]]

Drugim przykładem jest [Pieter Levels](https://x.com/levelsio) i jego projekt [PhotoAI](https://photoai.com/) oraz [InteriorAI](https://interiorai.com). Adresują one konkretne problemy i potwierdzają swoją użyteczność poprzez statystki publikowane przez Pietera. 

![[f127b451151792c9c592f21b671d61a0_MD5.png]]

Powyższe projekty wymieniam, aby nakreślić potencjalne obszary, którymi możemy się zająć i które mogą nas zachęcić do zainteresowania się generatywną grafiką. Tym bardziej, że nie musimy od razu tworzyć nowych produktów, ale nawet skorzystać z wybranych modeli na potrzeby funkcjonalności aplikacji, które już teraz rozwijamy.
## Obecne możliwości generowania obrazu

Rozwój generatywnej grafiki świetnie przedstawia postęp, który dokonał się na przestrzeni 2 ostatnich lat. Poniższa grafika pochodzi z wpisu [Comparing AI-generated images two years apart — 2022 vs. 2024](https://medium.com/@junehao/comparing-ai-generated-images-two-years-apart-2022-vs-2024-6c3c4670b905) i jasno widać z niej, że w 2022 roku trudno było mówić o poważnym zastosowaniu tych modeli. Dziś wygląda to zupełnie inaczej, choć nadal mówimy jeszcze o wielu ograniczeniach.

![[98a29a33807d43028bbd654f9568f98e_MD5.png]]

Jednym z takich ograniczeń jest zdolność modelu do generowania elementów obrazu takich jak tekst, dłonie, zęby czy lustrzane odbicie. I choć obecnie dostępne modele takie jak [Flux](glossary/Flux.md) radzą sobie z tymi zadaniami coraz lepiej, to nadal trudno jest mówić o powtarzalnych rezultatach. 

![[2ff5d47be63987f94391238788521a0f_MD5.png]]

Przeciętnie wypada także podążanie za instrukcjami, o czym już pisałem w lekcji [S01E03 — Limity](S01E03%20—%20Limity.md). Dlatego im bardziej złożony [prompt](glossary/Prompt.md) opisujący grafikę, tym mniejsze prawdopodobieństwo, że otrzymamy rezultat zgodny z oczekiwaniami.

Nie zmienia to jednak faktu, że jakość generowanych obrazów jest już teraz bardzo wysoka. Choć dojście do pożądanego efektu wymaga wielu prób, z pewnością jest to możliwe. Tym bardziej, że nie zawsze będzie nam zależało na tworzeniu kompleksowego obrazu, lecz pojedynczych elementów (np. tekstury czy tła) albo edycji istniejącej już grafiki czy zdjęcia. Poniżej nawet mamy prosty przykład [ComfyUI](ComfyUI), które zamienia moją twarz na zdjęciu wygenerowanym w [Midjourney](tools/Midjourney.md). 

![[3ee2c6662d5d62e7b33709f04a1e988a_MD5.png]]

Z programistycznego punktu widzenia, będzie nas interesowała dostępność modeli przez API lub ich samodzielny hosting. W tym pierwszym przypadku, naszą uwagę powinny zwrócić usługi takie jak wspomniana platforma [Replicate](tools/Replicate.md), a także [Leonardo.ai](https://leonardo.ai/). Z kolei w drugim, może nas zainteresować [RunPod](https://blog.runpod.io/how-to-get-stable-diffusion-set-up-with-comfyui-on-runpod/) lub podobne platformy oferujące dostęp do GPU.

Poza samą manipulacją obrazem, przydatne jest także posługiwanie się szablonami, na podstawie których będziemy generować grafiki. Jest to zwykle konieczne na potrzeby marketingowe, np. generowania kreacji reklamowych, okładek artykułów na bloga czy newslettera. Zwykle potrzebujemy tej samej kreacji w różnych formatach, których ręczne opracowanie jest bardzo czasochłonne. Poniżej mamy przykład szablonów okładek wydarzeń i kursów publikowanych na eduweb.pl. Aby wygenerować nowy zestaw, wystarczy podmienić zdjęcie i tekst w głównym komponencie, a zmiany zostaną odwzorowane na wszystkich pozostałych instancjach.

![[3cf38b599758d8ac72f2f6a913fa2f98_MD5.png]]

Obecnie sterowność modeli generujących grafiki jest dość ograniczona, ale można opracować prompty składające się zarówno z instrukcji tekstowych, jak i grafik referencyjnych. Pozwala to na zachowanie spójności stylu, co jest często wymagane w kontekście tonu marki czy wymagań projektu. Poniżej przykład okładek, które wykorzystywałem w jednym z moich projektów. 

![[804b265a1d2cec13d076b3ab096cd997_MD5.png]]

Znacznie większą sterowność można także uzyskać w [ComfyUI](ComfyUI), natomiast faktyczny wpływ na generowaną grafikę zależy od konfiguracji samego workflow oraz naszych potrzeb. 

Podsumowując, modele z obszaru generatywnej grafiki znacznie wzbogacają możliwości manipulacji i kreacji obrazów, a które jeszcze do niedawna były niemożliwe lub bardzo ograniczone. Pozwala nam to na: 

- Zwiększanie skali obrazu z (ograniczonym) zachowaniem detali
- Zwiększanie skali obrazu z powiększeniem kadru (przykładem jest Generative Expand dostępna w Photoshopie)
- Automatyczne usuwanie tła, również w trudnych przypadkach (np. włosy, cienie, krople)
- Usuwanie wybranych elementów zdjęcia (np. tła), zamianę ich z innymi oraz łączenie wielu zdjęć
- Generowanie spójnych obrazów, zgodnych z wymaganiami marki opisanymi w brandbooku
- Wykorzystywanie istniejących grafik do automatycznego generowania wielu formatów
- Tworzenie przybliżonych wizualizacji na podstawie opisów i grafik referencyjnych
- Animacje grafik do formy wideo (np. dzięki [Runway](https://runwayml.com/) [Heygen](https://www.heygen.com/), czy [Kling AI](https://klingai.com/))
- ...i wiele innych.
## Techniki projektowania promptów dla modeli

Generowanie grafik podobnie jak w przypadku [LLM](glossary/LLM.md) wymaga napisania [promptu](glossary/Prompt.md), aczkolwiek sama ich treść znacznie się różni, ponieważ zamiast pełnych instrukcji, potrzebujemy raczej słów kluczowych oraz flag sterujących ustawieniami. Widać to na przykładzie promptu [Midjourney](tools/Midjourney.md) w publicznej galerii użytkownika `kvovoorde`. Widać w nim szczegółowy opis sceny z uwzględnieniem słów kluczowych takich jak `shiny`, `dark blue`, `warm weather`, `natural lighting`. 

![[aae3a506b9455d9ce08ed901196fd48e_MD5.png]]

Z kolei inny przykład równie świetnej grafiki, posługuje się wyłącznie słowami kluczowymi, takimi jak `vibrant colors`, `cloes-up`, `black cat`. Widać także, że model nie uwzględnił wszystkich z wymienionych słów. 

![[2d987d97bab9f699354399b2f45b0c6d_MD5.png]]

Ogólna rekomendacja w przypadku [Midjourney](tools/Midjourney.md) mówi, aby prompty były krótkie i zawierały minimum informacji opisujących oczekiwany wynik. Jednak przegląd publicznie dostępnej galerii użytkowników sugeruje, że nie zawsze jest to prawda i znacznie lepiej jest eksperymentować. Nikt też nie powiedział, że nie możemy łączyć ze sobą różnych strategii. 

![[92182e8bc58761e29578cc142d312cb4_MD5.png]]

Poniżej widzimy prostą wizualizację zielonego dymu na czarnym tle, wygenerowanego modelem `niji`, który charakteryzuje styl anime. Sam prompt to zaledwie kilka słów, ale też pozornie trudno jest mówić o szczególnym dopasowaniu do moich potrzeb. 

![[11006bdd7047089db3ab6bc200e60a10_MD5.png]]

Na tym etapie detale nie miały większego znaczenia. Bardziej zależało mi na uzyskaniu ogólnego stylu, który będzie stanowić referencję dla dalszych grafik. Tutaj korzystając z pomocy modelu, zamieniłem uproszczony opis na precyzyjną wizję tego, co chcę uzyskać. 

![[0b5f1db57dbab05380cb8f4648c7844c_MD5.png]]

Powstała więc pierwsza wersja wizualizująca awatary w stylu, który przypadł mi do gustu. Jest to zatem dobra podstawa do generowania kolejnych grafik. Co więcej, prompt, który wykorzystałem do stworzenia pierwszej wersji, ma charakter [meta promptu](glossary/Meta%20Prompt.md). Oznacza to, że możemy wygodnie użyć go do generowania kolejnych awatarów. 

![[6a369b212ff019876fccb27527d828e9_MD5.png]]

Konkretnie, prompt zawiera stałe elementy, ale też daje możliwość podmiany fragmentu opisującego samą postać. Widać to na poniższym screenie, gdzie oznaczyłem go placeholderem `[DESC]`. Tutaj ponownie miałem ogólny pomysł na to, jakich postaci potrzebuję, ale skorzystałem z pomocy modelu, aby wygenerować bogatszy w słowa kluczowe opis. Poza tym, do samej wiadomości dołączyłem także grafikę prezentującą pierwszą wersję awatarów. 

![[45f520fa7400b5e4849c47aa21ca99ed_MD5.png]]

Rezultat w postaci pierwszej iteracji widać poniżej i dalsze próby będą zależały już od naszych idywidualnych preferencji. Widzimy jednak, że spójny styl został zachowany w przypadku każdej z postaci, wyłączając pojedyncze grafiki, które wykraczają poza paletę kolorów. 

![[a04bb7eeb4319363879d13aad9ef8b3d_MD5.png]]

Na tym jednak nie koniec, ponieważ wypracowany styl możemy połączyć także z istniejącymi już grafikami czy nawet zdjęciami. W przypadku większości popularnych narzędzi do generatywnej grafiki mamy możliwość dołączenia postaci, która ma zostać odwzorowana przez model. Jak widać na przykładzie `Alice`, rezultaty są w porządku na tyle, że spośród nich możemy wybrać ten, który będzie odpowiadał nam najbardziej. 

![[fc347223eace57747758bfdbae528328_MD5.png]]

Choć sam zdecydowałem się w tym przypadku na styl ilustracji, to nic nie stoi na przeszkodzie, aby wybrać inne, w tym także bardzo realistyczny. 

[Midjourney](tools/Midjourney.md), za pomocą którego wygenerowałem powyższe grafiki, charakteryzuje się świetną jakością, ale bardzo niską sterownością. Jednak największym problemem jest brak oficjalnego API (nieoficjalne wrappery mogą doprowadzić do zablokowania konta). Pomimo tego, **wszystkie powyższe techniki** można zastosować w połączeniu z [ComfyUI](ComfyUI) lub podobnymi narzędziami. Mam tutaj na myśli przede wszystkim: **nadawanie stylu, meta prompty oraz obrazy referencyjne**. Przykładem tego może być poniższy workflow, który pokazuje to w praktyce. Oczywiście w związku z zastosowaniem innego modelu, efekt różni się od wcześniejszego, natomiast schemat pozostaje taki sam. 

![[c6430623ad313cf0e9f1bdb79cc7ebb0_MD5.png]]
## Generowanie grafik w oparciu o szablony

Jak widać, [ComfyUI](ComfyUI) daje ogromne możliwości wpływania na kształt generowanych grafik. Jednak w praktyce może okazać się to niewystarczające, szczególnie gdy będzie nam zależało na bardzo konkretnych szablonach. 

Tutaj z pomocą przychodzą rozwiązania takie jak [htmlcsstoimage](https://htmlcsstoimage.com), które pozwalają na generowanie grafik z pomocą API, na podstawie szablonów HTML. Mamy więc możliwość dynamicznego podmieniania tekstów oraz grafik, a nawet stylów CSS. Natomiast teraz wchodzą do gry dwa dodatkowe elementy — [Vision Language Models](glossary/Vision%20Language%20Models.md) oraz generatywna grafika.

![[522004e572c96ead073d7ed3163553de_MD5.png]]

Możemy zatem: 

- Zdefiniować szablon HTML, zawierający określoną kolorystykę, fonty i ogólny układ, wliczając w to także responsywność oraz dopasowanie zachowania w zależności od rozmiaru elementów (np. ilości tekstu)
- Zbudować workflow [ComfyUI](ComfyUI) i/lub prompty do innych narzędzi generujących grafiki lub elementy szablonów poprzez API
- Stworzyć aplikację, która reaguje na zdarzenia takie jak dodanie do kolejki posta social media, wpisu na bloga czy newslettera, a następnie tworzy serię grafik i przekazuje je do weryfikacji

Taki schemat (z wyłączeniem generowanych grafik, które wtedy jeszcze nie były dostępne) stosowaliśmy przez niemal 3 lata w eduweb.pl, generując w ten sposób materiały promocyjne 5 różnych wydań newslettera. Grafiki dopasowywały się do autora lub autorki, a także specjalizacji oraz treści samego newslettera. 

![[26ea7a0f589ec4a84d44e0e992adef00_MD5.png]]

Pomimo responsywności, powyższe szablony były jednak dość statyczne ze względu na potrzebę ograniczenia interwencji ze strony użytkownika. Obecnie możemy pozwolić sobie na znacznie więcej, ponieważ część błędów może automatycznie naprawić model.
## Podsumowanie

Narzędzia z obszaru generatywnej grafiki pozwalają na tworzenie automatyzacji oraz wyspecjalizowanych narzędzi zdolnych do transformacji obrazów według zdefiniowanego stylu. Z tego powodu warto zainteresować się nimi, nawet jeśli sami bezpośrednio nie jesteśmy zaangażowani w procesy związane z grafiką. 

Spośród wszystkich wymienionych dzisiaj rozwiązań, na szczególną uwagę zasługują [ComfyUI](ComfyUI) oraz [HTMLCSStoImage](https://htmlcsstoimage.com/), ponieważ mocno przecinają się one z obszarem programowania. Z ich pomocą możemy budować zaawansowane rozwiązania zdolne do wsparcia lub nawet automatyzacji elementów procesu marketingowego czy produktowego. Ostatecznie wartość wiedzy na temat budowania programistycznych rozwiązań, które wykorzystują modele generatywnej grafiki, wystarczająco dużo mówią przykłady produktów Pietera Levelsa z początku tej lekcji. W sieci można spotkać także inne zastosowania, bezpośrednio związane z procesem projektowym, tworzenia reklam, czy edycji zdjęć. 

**WAŻNE:** Jeśli nie posiadasz komputera, który pozwoli na swobodną pracę z ComfyUI i nie chcesz korzystać z płatnych narzędzi, to możesz pominąć poniższy film. 

<div style="padding:75% 0 0 0;position:relative;"><iframe src="https://player.vimeo.com/video/1029104946?badge=0&amp;autopause=0&amp;player_id=0&amp;app_id=58479" frameborder="0" allow="autoplay; fullscreen; picture-in-picture; clipboard-write" style="position:absolute;top:0;left:0;width:100%;height:100%;" title="02_03_comfy"></iframe></div><script src="https://player.vimeo.com/api/player.js"></script>

Powodzenia!](<Claro, aqui está a tradução do texto para português do Brasil:

Título: [[Sem título 6]]
Caminho: Sem título 6.md

![[d5014260581b55e554178704c68ad087_MD5.png]]

Tivemos a oportunidade de constatar as capacidades da IA generativa no processamento de texto e áudio, bem como a capacidade de interpretar imagens. Agora, veremos quais opções temos no contexto de manipulação e geração de novos gráficos e fotos.

O design de criações gráficas e o trabalho com fotos até agora não estavam diretamente associados à programação, com exceção do desenvolvimento de ferramentas para este setor ou da construção de interações avançadas com HTML Canvas e WebGL. Parece, portanto, que, na era da IA generativa, são as pessoas envolvidas no design ou na criação de ilustrações que deveriam estar interessadas em ferramentas como [Midjourney](tools/Midjourney.md) ou [Stable Diffusion](glossary/Stable%20Diffusion.md). No entanto, verifica-se que não é bem assim.

Um exemplo é a ferramenta [picthing](https://pic.ping.gg/), que permite remover eficazmente o fundo das fotos, construída pelo criador do canal `Theo — t3.gg`. Embora a remoção do fundo em si não seja algo novo, aqui estamos a falar de um aumento significativo na qualidade. Acima de tudo, no entanto, este projeto é um exemplo de como a IA generativa pode ser usada para construir produtos úteis.

![[0d5ccbf9935bfe0209bcc5698ae8d4a7_MD5.png]]

O segundo exemplo é [Pieter Levels](https://x.com/levelsio) e o seu projeto [PhotoAI](https://photoai.com/) e [InteriorAI](https://interiorai.com). Eles abordam problemas específicos e confirmam a sua utilidade através de estatísticas publicadas por Pieter.

![[f127b451151792c9c592f21b671d61a0_MD5.png]]

Menciono os projetos acima para delinear as áreas potenciais que podemos abordar e que podem nos encorajar a nos interessarmos por gráficos generativos. Especialmente porque não precisamos criar novos produtos imediatamente, mas até mesmo usar modelos selecionados para as necessidades de funcionalidade de aplicativos que já estamos desenvolvendo.

## Capacidades atuais de geração de imagem

O desenvolvimento de gráficos generativos mostra perfeitamente o progresso que foi feito nos últimos 2 anos. O gráfico abaixo é da postagem [Comparing AI-generated images two years apart — 2022 vs. 2024](https://medium.com/@junehao/comparing-ai-generated-images-two-years-apart-2022-vs-2024-6c3c4670b905) e mostra claramente que em 2022 era difícil falar sobre o uso sério desses modelos. Hoje, parece completamente diferente, embora ainda estejamos a falar de muitas limitações.

![[98a29a33807d43028bbd654f9568f98e_MD5.png]]

Uma dessas limitações é a capacidade do modelo de gerar elementos de imagem, como texto, mãos, dentes ou reflexos espelhados. E embora os modelos atualmente disponíveis, como [Flux](glossary/Flux.md), estejam a lidar com essas tarefas cada vez melhor, ainda é difícil falar sobre resultados repetíveis.

![[2ff5d47be63987f94391238788521a0f_MD5.png]]

Seguir as instruções também é medíocre, como escrevi na lição [S01E03 — Limity](S01E03%20—%20Limity.md). Portanto, quanto mais complexo for o [prompt](glossary/Prompt.md) que descreve os gráficos, menor a probabilidade de obtermos um resultado que atenda às expectativas.

Isso não muda o fato de que a qualidade das imagens geradas já é muito alta. Embora chegar ao efeito desejado exija muitas tentativas, certamente é possível. Especialmente porque nem sempre estaremos interessados em criar uma imagem complexa, mas sim elementos individuais (por exemplo, texturas ou fundos) ou editar gráficos ou fotos existentes. Abaixo, temos até um exemplo simples de [ComfyUI](ComfyUI), que transforma meu rosto numa foto gerada no [Midjourney](tools/Midjourney.md).

![[3ee2c6662d5d62e7b33709f04a1e988a_MD5.png]]

Do ponto de vista da programação, estaremos interessados na disponibilidade de modelos através de API ou sua hospedagem independente. No primeiro caso, a nossa atenção deve ser atraída por serviços como a plataforma [Replicate](tools/Replicate.md) mencionada, bem como [Leonardo.ai](https://leonardo.ai/). Por outro lado, no segundo caso, podemos estar interessados em [RunPod](https://blog.runpod.io/how-to-get-stable-diffusion-set-up-with-comfyui-on-runpod/) ou plataformas semelhantes que oferecem acesso a GPUs.

Além da manipulação da imagem em si, também é útil usar modelos com base nos quais geraremos gráficos. Isso geralmente é necessário para fins de marketing, por exemplo, gerar criações de publicidade, capas de artigos de blog ou newsletters. Normalmente, precisamos da mesma criação em diferentes formatos, cujo desenvolvimento manual é muito demorado. Abaixo, temos um exemplo de modelos de capa de eventos e cursos publicados no eduweb.pl. Para gerar um novo conjunto, basta substituir a foto e o texto no componente principal, e as alterações serão refletidas em todas as outras instâncias.

![[3cf38b599758d8ac72f2f6a913fa2f98_MD5.png]]

Atualmente, o controlo dos modelos que geram gráficos é bastante limitado, mas podemos desenvolver prompts que consistem tanto em instruções de texto quanto em gráficos de referência. Isso permite manter a consistência do estilo, o que geralmente é necessário no contexto do tom da marca ou dos requisitos do projeto. Abaixo, um exemplo de capas que usei num dos meus projetos.

![[804b265a1d2cec13d076b3ab096cd997_MD5.png]]

Um controlo muito maior também pode ser obtido no [ComfyUI](ComfyUI), enquanto o impacto real nos gráficos gerados depende da configuração do próprio fluxo de trabalho e das nossas necessidades.

Em resumo, os modelos na área de gráficos generativos enriquecem significativamente as possibilidades de manipulação e criação de imagens, que até recentemente eram impossíveis ou muito limitadas. Isso nos permite:

- Aumentar a escala da imagem com (limitada) preservação de detalhes
- Aumentar a escala da imagem com ampliação do quadro (um exemplo é o Generative Expand disponível no Photoshop)
- Remoção automática do fundo, também em casos difíceis (por exemplo, cabelo, sombras, gotas)
- Remover elementos selecionados de uma foto (por exemplo, fundo), substituí-los por outros e combinar várias fotos
- Gerar imagens consistentes, consistentes com os requisitos da marca descritos no brandbook
- Usar gráficos existentes para gerar automaticamente muitos formatos
- Criar visualizações aproximadas com base em descrições e gráficos de referência
- Animações de gráficos para a forma de vídeo (por exemplo, graças a [Runway](https://runwayml.com/) [Heygen](https://www.heygen.com/) ou [Kling AI](https://klingai.com/))
- ...e muitos outros.

## Técnicas de design de prompts para modelos

Gerar gráficos, como no caso de [LLM](glossary/LLM.md), requer escrever um [prompt](glossary/Prompt.md), embora o seu conteúdo em si seja muito diferente, porque em vez de instruções completas, precisamos de palavras-chave e sinalizadores que controlem as configurações. Isso pode ser visto no exemplo do prompt [Midjourney](tools/Midjourney.md) na galeria pública do usuário `kvovoorde`. Podemos ver uma descrição detalhada da cena, incluindo palavras-chave como `shiny`, `dark blue`, `warm weather`, `natural lighting`.

![[aae3a506b9455d9ce08ed901196fd48e_MD5.png]]

Por outro lado, outro exemplo de gráficos igualmente excelentes usa apenas palavras-chave, como `vibrant colors`, `cloes-up`, `black cat`. Também pode ser visto que o modelo não levou em consideração todas as palavras mencionadas.

![[2d987d97bab9f699354399b2f45b0c6d_MD5.png]]

A recomendação geral no caso do [Midjourney](tools/Midjourney.md) é que os prompts sejam curtos e contenham o mínimo de informações que descrevam o resultado esperado. No entanto, uma revisão da galeria de usuários disponível publicamente sugere que nem sempre é verdade e é muito melhor experimentar. Ninguém disse que não podemos combinar diferentes estratégias.

![[92182e8bc58761e29578cc142d312cb4_MD5.png]]

Abaixo, vemos uma visualização simples de fumaça verde num fundo preto, gerada pelo modelo `niji`, que é caracterizado pelo estilo anime. O prompt em si tem apenas algumas palavras, mas também é aparentemente difícil falar sobre uma correspondência específica com as minhas necessidades.

![[11006bdd7047089db3ab6bc200e60a10_MD5.png]]

Nesta fase, os detalhes não importavam muito. Eu estava mais interessado em obter um estilo geral que servisse de referência para gráficos adicionais. Aqui, com a ajuda do modelo, transformei uma descrição simplificada numa visão precisa do que quero obter.

![[0b5f1db57dbab05380cb8f4648c7844c_MD5.png]]

Assim, foi criada a primeira versão que visualiza avatares num estilo que eu gostei. Esta é, portanto, uma boa base para gerar gráficos adicionais. Além disso, o prompt que usei para criar a primeira versão é um [meta prompt](glossary/Meta%20Prompt.md). Isso significa que podemos usá-lo convenientemente para gerar avatares adicionais.

![[6a369b212ff019876fccb27527d828e9_MD5.png]]

Especificamente, o prompt contém elementos fixos, mas também permite substituir um fragmento que descreve o personagem em si. Isso pode ser visto na captura de tela abaixo, onde marquei com o marcador de posição `[DESC]`. Aqui, novamente, eu tinha uma ideia geral de que tipo de personagens eu precisava, mas usei a ajuda do modelo para gerar uma descrição mais rica em palavras-chave. Além disso, também anexei um gráfico mostrando a primeira versão dos avatares à mensagem.

![[45f520fa7400b5e4849c47aa21ca99ed_MD5.png]]

O resultado na forma da primeira iteração pode ser visto abaixo e tentativas adicionais já dependerão das nossas preferências individuais. No entanto, vemos que um estilo consistente foi mantido no caso de cada personagem, excluindo gráficos individuais que estão fora da paleta de cores.

![[a04bb7eeb4319363879d13aad9ef8b3d_MD5.png]]

Mas isso não é tudo, porque o estilo desenvolvido também pode ser combinado com gráficos ou até fotos existentes. No caso da maioria das ferramentas populares para gráficos generativos, temos a capacidade de anexar um personagem que deve ser reproduzido pelo modelo. Como pode ser visto no exemplo de `Alice`, os resultados são bons o suficiente para que possamos escolher aquele que melhor nos convier.

![[fc347223eace57747758bfdbae528328_MD5.png]]

Embora eu mesmo tenha decidido neste caso pelo estilo de ilustração, nada impede que escolha outros, incluindo um muito realista.

[Midjourney](tools/Midjourney.md), com o qual gerei os gráficos acima, é caracterizado por excelente qualidade, mas controlo muito baixo. No entanto, o maior problema é a falta de uma API oficial (wrappers não oficiais podem levar ao bloqueio da conta). Apesar disso, **todas as técnicas acima** podem ser aplicadas em combinação com [ComfyUI](ComfyUI) ou ferramentas semelhantes. Refiro-me aqui principalmente a: **atribuição de estilo, meta prompts e imagens de referência**. Um exemplo disso pode ser o seguinte fluxo de trabalho, que mostra isso na prática. Obviamente, devido ao uso de um modelo diferente, o efeito é diferente do anterior, mas o esquema permanece o mesmo.

![[c6430623ad313cf0e9f1bdb79cc7ebb0_MD5.png]]

## Gerando gráficos com base em modelos

Como pode ser visto, [ComfyUI](ComfyUI) oferece enormes possibilidades de influenciar a forma dos gráficos gerados. No entanto, na prática, isso pode não ser suficiente, especialmente quando nos importamos com modelos muito específicos.

Aqui, soluções como [htmlcsstoimage](https://htmlcsstoimage.com) vêm em socorro, permitindo gerar gráficos com a ajuda de uma API, com base em modelos HTML. Portanto, temos a capacidade de substituir dinamicamente textos e gráficos, e até estilos CSS. No entanto, agora dois elementos adicionais entram em jogo — [Vision Language Models](glossary/Vision%20Language%20Models.md) e gráficos generativos.

![[522004e572c96ead073d7ed3163553de_MD5.png]]

Portanto, podemos:

- Definir um modelo HTML, contendo cores, fontes e layout geral específicos, incluindo responsividade e ajuste de comportamento dependendo do tamanho dos elementos (por exemplo, quantidade de texto)
- Construir um fluxo de trabalho [ComfyUI](ComfyUI) e/ou prompts para outras ferramentas que geram gráficos ou elementos de modelos através de API
- Criar um aplicativo que reage a eventos como adicionar uma postagem de mídia social, postagem de blog ou newsletter à fila e, em seguida, cria uma série de gráficos e os envia para verificação

Este esquema (excluindo gráficos gerados, que não estavam disponíveis na época) foi usado por quase 3 anos no eduweb.pl, gerando materiais promocionais para 5 edições diferentes de newsletter desta forma. Os gráficos foram adaptados ao autor ou autora, bem como à especialização e ao conteúdo da própria newsletter.

![[26ea7a0f589ec4a84d44e0e992adef00_MD5.png]]

Apesar da responsividade, os modelos acima eram bastante estáticos devido à necessidade de limitar a intervenção do usuário. Atualmente, podemos nos permitir muito mais, porque parte dos erros pode ser corrigida automaticamente pelo modelo.

## Resumo

As ferramentas na área de gráficos generativos permitem criar automação e ferramentas especializadas capazes de transformar imagens de acordo com um estilo definido. Por esse motivo, vale a pena se interessar por elas, mesmo que não estejamos diretamente envolvidos em processos relacionados a gráficos.

De todas as soluções mencionadas hoje, [ComfyUI](ComfyUI) e [HTMLCSStoImage](https://htmlcsstoimage.com/) merecem atenção especial, porque se cruzam fortemente com a área de programação. Com a sua ajuda, podemos construir soluções avançadas capazes de apoiar ou até mesmo automatizar elementos do processo de marketing ou produto. Em última análise, o valor do conhecimento sobre a construção de soluções de programação que usam modelos de gráficos generativos é suficientemente demonstrado pelos exemplos de produtos de Pieter Levels do início desta lição. Na web, também pode encontrar outros usos, diretamente relacionados ao processo de design, criação de anúncios ou edição de fotos.

**IMPORTANTE:** Se não tiver um computador que permita trabalhar livremente com ComfyUI e não quiser usar ferramentas pagas, pode ignorar o vídeo abaixo.

%3Cdiv style="padding:75% 0 0 0;position:relative;"%3E<iframe src="https://player.vimeo.com/video/1029104946?badge=0&amp;autopause=0&amp;player_id=0&amp;app_id=58479" frameborder="0" allow="autoplay; fullscreen; picture-in-picture; clipboard-write" style="position:absolute;top:0;left:0;width:100%;height:100%;" title="02_03_comfy"></iframe></div><script src="https://player.vimeo.com/api/player.js"></script>

Boa sorte!>)