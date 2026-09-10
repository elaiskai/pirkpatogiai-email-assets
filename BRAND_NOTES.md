# PirkPatogiai — įkėlimas į Omnisend

## Horizontali pop-up nuotrauka — 2026-09-10

Pagal faktinį vartotojo Omnisend išdėstymą vaizdas dedamas virš formos, todėl sukurtas žemas, platus `assets/campaign/popup-namai-horizontal.jpg` (1600 × 600 px, 8:3). Ankstesnis vertikalus kadras paliktas kaip alternatyva šoninei kompozicijai. Naujas vaizdas sukurtas integruotu ImageGen įrankiu: scena išplėsta ir perkomponuota, išlaikant baldų tapatybę, dienos šviesą ir brando spalvas. Baigiamasis failas eksportuotas optimizuotu JPG formatu. Formoje vaizdo aukštis turi prisitaikyti automatiškai.

<details><summary>Horizontalios versijos generavimo užduotis</summary>

Use case: precise-object-edit / ads-marketing. Edit the reference interior photograph into a WIDE LOW HORIZONTAL POPUP BANNER. Required canvas aspect ratio EXACTLY 8:3 (2.6667:1), target 1600 pixels wide by 600 pixels high. This is a panoramic landscape image, absolutely NOT portrait, square, or standard 4:3. The banner will sit ABOVE an email signup form, so it must be low and wide. Keep the same warm natural editorial photography, olive-taupe corduroy Brook Cord chair with its stitched panels and FOUR natural beech legs, Edduma two-tier round pale oak coffee table with slender black metal supports, fresh yellow-green wall, sheer ivory curtains, pale oak floor, cream textured rug, and gentle sunlight. Zoom the camera OUT and widen the room horizontally. Recompose the COMPLETE chair, from top of back to feet, at about x=35% of the wide frame, occupying around 70–80% of image height. Place the COMPLETE round coffee table at x=64%, a little lower, in correct natural proportions. The wider room extends to both sides with a restrained leafy plant at far left and softly lit green wall at right. The exact furniture designs, panel seams, wood shapes, round tabletops, and black table posts must remain faithful to the original. Keep a cream cup, a simple vase with a small leafy branch, and one plain book as restrained styling. Maintain believable contact shadows and a realistic camera perspective. Leave generous horizontal breathing room; keep all important furniture comfortably away from the frame edges so a tiny crop does not cut it. Do not stretch the original photograph, do not just slice through the chair, do not chop furniture legs. Create a complete coherent wide room scene. No text, no letters, no numbers, no coupon, no logos, no watermark, no UI or white border. Full-bleed photograph on a strict 1600x600 wide canvas.

</details>


**3 laiškai · 10 € · LABAS10 · atnaujinta 2026-09-10**

Brando analizė, tekstų kryptis, šaltiniai ir laiškų temos pateikti [BRAND_DNA.md](BRAND_DNA.md). Visų laiškų peržiūra — [PERZIURA.html](PERZIURA.html).

## Kokius failus naudoti

| Failai | Paskirtis |
|---|---|
| `01-labas-namai.html`, `02-tavo-ritmui.html`, `03-issirink-patogiau.html` | Pilni HTML laiškai su dokumento antrašte ir mobiliais stiliais |
| `omnisend/01-labas-namai.html` ir atitinkami 02, 03 failai | Turinys Omnisend Custom HTML laukui; be DOCTYPE, head ir body žymų |
| `omnisend/styles.css` | Bendri stiliai, skirti HTML bloko **Styles** laukui |
| Atitinkami `.txt` failai | Laiškų temos, preheaderiai ir tekstinės versijos |
| `previews/` | Vietinės peržiūros ir kompiuterio / telefono ekrano vaizdai |
| `assets/` | Oficialios produktų nuotraukos, logotipas ir 3 optimizuoti hero |

## Įkelti kiekvieną laišką

1. Savo welcome automatizacijoje atidaryk atitinkamą el. laišką ir įrašyk temą bei preheaderį iš BRAND_DNA arba `.txt` failo.
2. Pasirink tuščią maketą. Turinio plotis — **600 px**, išorinės Custom HTML bloko paraštės — **0**, kad hero eitų per visą laiško plotį. HTML automatiškai prisitaiko ir prie siauresnio bloko su paraštėmis. Pašalink papildomus numatyto maketo logotipus ir tekstus.
3. Įdėk **Custom HTML** elementą. Į HTML lauką nukopijuok visą atitinkamo `omnisend/0x-....html` failo turinį.
4. Į **Styles** lauką įklijuok `omnisend/styles.css`. Tai pritaiko tarpus, šriftų dydžius ir korteles telefonui. Pagrindinis laiško ir vaizdų plotis prisitaiko ir be šio lauko. CSS apribotas laiško elementais, kad nepakeistų aplinkinio Omnisend maketo.
5. **Repozitorija vieša.** Visi 3 hero vaizdai pasiekiami laiškų HTML jau įrašytais `raw.githubusercontent.com` adresais; kiekvienas patikrintas be prisijungimo ir grąžina teisingą JPEG vaizdą. Produktų nuotraukos bei logotipas naudoja viešus parduotuvės adresus. Papildomai kelti hero į „Omnisend“ nereikia. Išsaugok laišką ir atnaujink „Omnisend“ peržiūrą. Vietinė PERZIURA.html bei `previews/*-local.html` peržiūra taip pat veikia. Repozitorija turi likti vieša, o naudojami vaizdai — prieinami tais pačiais keliais.
6. Palik Omnisend paskyros siuntėjo duomenis ir reikiamą poraštę su tikru įmonės adresu. Laiškų HTML turi patvirtintą Omnisend žymą `[[ unsubscribe_link ]]`; patikrink, kad ji išsisprendžia. Jei platforma prideda antrą atsisakymo eilutę, suvienodink poraštės tekstą redaktoriuje, išlaikydamas veikiančią atsisakymo nuorodą.

HTML teksto pakeitimai atliekami Custom HTML bloke. Tai nėra iš atskirų Omnisend produktų blokų sudėtas šablonas. Produktų pasirinkimas šioje versijoje nėra dinaminis. Kainos nerodomos; jų aktualumą žmogus mato produkto puslapyje.

Oficialios instrukcijos: [Custom HTML ir Styles laukai](https://support.omnisend.com/en/articles/1061866-add-configure-custom-html-item), [HTML importas](https://support.omnisend.com/en/articles/2964086-import-custom-html-email-templates), [personalizavimo žymos](https://support.omnisend.com/en/articles/11197418-use-liquid-templating-for-message-personalization).

## Automatizacijos nustatymai

Rekomenduojama seka:

**Nauja prenumerata → 01 laiškas → laukti 1 dieną → 02 laiškas → laukti 2 dienas → 03 laiškas.**

- Trigger: **Subscribed to Marketing**.
- Filtrai: **Channel subscribed to = Email** ir **First subscription = true**.
- Šaltinius susiek su formomis / integracija, kurios žada LABAS10 pasiūlymą. Patikrink realaus testinio kontakto prenumeratos šaltinį: vien „Signup form“ filtras gali atmesti per kitą integraciją perduotą kontaktą.
- Kanalas: tik kontaktai, užsiprenumeravę el. pašto rinkodarą.
- Išėjimo sąlyga: **Placed order**, jei šį įvykį perduoda parduotuvės integracija. Taip įsigijęs žmogus nebegaus likusių welcome priminimų. Užsakymo įvykio gavimą patikrink praktiškai prieš remdamasis šia sąlyga.
- Ši seka skirta naujiems prenumeratoriams. Esamų kontaktų masiškai į ją neįtrauk.

Jeigu LABAS10 vėliau bus patvirtintas kaip tik pirmo pirkimo pasiūlymas, papildomai atskirk jau pirkusius kontaktus pagal tikrus Omnisend užsakymų duomenis. Dabartiniuose tekstuose pirmo pirkimo apribojimas neteigiamas.

Šaltiniai: [Welcome Automation](https://support.omnisend.com/en/articles/9653272-welcome-automation), [Exit Conditions / Automation FAQ](https://support.omnisend.com/en/articles/4315344-automation-faq).

## Prieš įjungiant

- Patikrink, kad parduotuvėje veikia **LABAS10 → 10 €** ir pasiūlymas sutampa su prenumeratos forma. Minimalios sumos, išimtys bei terminas nebuvo pateikti.
- Nustatyk patvirtintą parduotuvės siuntėją ir tikrus paskyros / įmonės duomenis Omnisend poraštėje.
- Atlik testinę prenumeratą su nauju adresu ir patikrink gautą laišką bei atsisakymo nuorodą. Šios užduoties metu laiškai nebuvo importuoti į tavo Omnisend paskyrą ar išsiųsti.
- Patikrink, kad atlikus užsakymą kontaktas išeina iš šios serijos.

Svetainės turinys ir galimi pirkimo duomenys nesuteikė pagrindo naudoti atsiliepimus, perkamiausių prekių etiketes ar kupono galiojimo atgalinį skaičiavimą.

## Vizualai ir struktūra

- **01:** didelis valgomojo hero su „Brook Cord“, 10 € pasiūlymas, 8 produktai ir blokas apie atskirų namų kampelių atnaujinimą.
- **02:** darbo vietos hero su „Billings“ ir „Rako“, 4 produktai, trys konkretūs patikrinimai prieš perkant baldus, nuolaidos priminimas.
- **03:** poilsio hero su „Elara“ ir „Corbitan“, kompaktiška LABAS10 juosta, 4 kiti produktai, pristatymo ir atsiskaitymo informacija.

Hero scenos sukurtos integruotu ImageGen įrankiu pagal tikras konkrečių produktų nuotraukas. Tai stilizuotos interjero vizualizacijos; produktų kortelėse paliktos oficialios parduotuvės nuotraukos. Scenų dekoras nėra parduodamo baldo komplektacijos pažadas. Prekių komplektaciją nurodo parduotuvės aprašymas.

Kūrybinės užduotys: šiltas šviesus valgomasis su „Brook Cord“ ir užrašu „LABAS, NAMAI.“; darbo vieta su „Billings“ bei „Rako“ ir užrašu „ERDVĖ, KURI TINKA TAU.“; ramus poilsio kampelis su „Elara“, „Corbitan“ ir užrašu „MAŽAS POKYTIS. DAUGIAU JAUKUMO.“. Visiems vaizdams naudotas žalsvas, grafito, šviesaus medžio ir baltos spalvų derinys, didelė aiški tipografika ir perėjimas į baltą apačioje. Antro hero korekcija atstatė tikrojo stalo atskirą lentynėlę virš pagrindinio stalviršio.

Failai: `assets/campaign/w1-hero.jpg` (1080 × 1440), `w2-hero.jpg` ir `w3-hero.jpg` (1080 × 1350). Kiekvienas sveria mažiau nei 360 KB. Atvaizdavimas laiške — 600 px pločio, telefone mažinamas proporcingai.

## Patikra

Laiškai vizualiai peržiūrėti 600 px turinio pločiu bei 390 ir 320 px mobiliuose ekranuose. Po peržiūros sumažinti tušti tarpai produktų kortelėse ir suvienodinti kortelių aukščiai. Kritiniai stiliai yra inline, visos lentelės turi presentation paskirtį, vaizdai — alt tekstus bei matmenis. Produktų ir navigacijos nuorodose naudojamos UTM žymos. Kupono galiojimo pabaiga, išimtys ir pardavimų reitingai neišgalvoti.

Hero vaizdų vieši adresai papildomai patikrinti be autentifikacijos: visi trys grąžino HTTP 200, `image/jpeg`, o jų turinys sutapo su vietiniais failais.

Tai naršyklės ir šaltinių patikra. Gautų Gmail, Apple Mail ir Outlook laiškų tikrinimas atliekamas po įkėlimo į Omnisend.

## Pop-up vaizdas — 2026-09-10

Failas: `assets/campaign/popup-namai.jpg`, 1080 × 1350 px, vertikalus 4:5 kadras be užrašų. Sukurtas integruotu ImageGen įrankiu pagal oficialias „Brook Cord“ ir „Edduma“ nuotraukas; optimizuotas JPG formatui. Naudojamas šalia prenumeratos formos. Pop-up tekstai: [POPUP_TEKSTAI.md](POPUP_TEKSTAI.md).

<details><summary>Galutinė vaizdo generavimo užduotis</summary>

Use case: ads-marketing. Asset type: standalone photographic side-panel image for a PirkPatogiai.lt email signup pop-up. Generate a new original portrait 4:5 interior photograph, approximately 1080x1350, with NO text, NO numbers, NO logos, NO watermark, NO popup or interface. Input image 1 is the exact Brook Cord chair identity reference: preserve its olive-taupe fine ribbed corduroy, upholstered shell with horizontal and vertical panel seams, gently curved backrest, and four splayed natural beech legs. Input image 2 is the exact Edduma round coffee table identity reference: preserve its pale oak 80 cm round top and lower shelf, slim black metal supports and real proportions. Scene: a quiet, welcoming Lithuanian / Scandinavian home corner, warm pale oak floor, textured ivory rug, a soft fresh yellow-green painted wall inspired by brand #C9E165, sheer off-white curtain at the left edge, gentle natural morning light and soft believable plant shadows. Composition: chair dominant in the center-left, complete silhouette with feet in frame; the low table beside it at the right, realistically scaled, perhaps slightly cropped at the right edge; just one simple cream ceramic cup and a closed unbranded book on the table, one restrained leafy branch or plant near the curtain. Frame tightly enough to feel inviting and detailed in a small pop-up side panel. Keep the meaningful furniture in the central 80 percent so modest cropping is safe. Refined editorial interior photography, true fabric texture and timber grain, natural lens perspective, realistic grounding shadows, restrained styling. The green wall occupies only the upper/background part; chair and coffee table provide the focal interest. Full-bleed photo to all four edges, no white fading bands, no graphic blocks, no text whatsoever. Do not invent or distort the furniture design. Do not make a website mockup.

</details>


## Pločio pataisymas pagal Omnisend ekrano vaizdą

Ankstesnė 600 px lentelė išsiplėsdavo už bloko, kai jo paraštės turiniui palikdavo tik 552 px. Visų 3 laiškų pagrindinė lentelė dabar turi `width="100%"`, inline `width:100%`, `max-width:600px` ir fiksuotą vidinių stulpelių išdėstymą. Hero, logotipas ir produktų nuotraukos prisitaiko prie turimos vietos. Pašalintas papildomas išorinis tarpas virš logotipo.

Norint pritaikyti pataisymą jau sukurtam laiškui, **pakeisk esamą Custom HTML turinį nauju failu iš `omnisend/` ir atnaujink Styles lauką**. GitHub pakeitimai automatiškai neperrašo anksčiau į Omnisend įklijuoto HTML. Hero adresai nesikeitė.

Patikrinta naršyklėje imituojant 600 ir 560 px Omnisend bloką su 24 px paraštėmis, 390 ir 320 px telefoną su 16 px paraštėmis, taip pat be papildomo Styles lauko kompiuterio bloke. Pradinė versija atkūrė pločio klaidą; pataisytos versijos telpa visais 18 tikrintų atvejų. Tai bloko modelio patikra, o ne tiesioginis Omnisend paskyros redagavimas.
