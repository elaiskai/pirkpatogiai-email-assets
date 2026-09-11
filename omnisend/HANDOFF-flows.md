# Pirk Patogiai · Automatizacijos (krepšelis / atsiskaitymas / naršymas) · Omnisend handoff

**Built:** 2026-09-09 (v1) · **Klientas:** PirkPatogiai.lt (Remigijus Stonkus, OpenCart) · **ESP:** Omnisend (API key dar negautas)
**Preview (Pages):** https://elaiskai.github.io/email-client-assets/pirkpatogiai/automations/
**Logo CDN:** `https://cdn.jsdelivr.net/gh/elaiskai/email-client-assets@main/pirkpatogiai/automations/logo-pirkpatogiai.png`
**Brand:** `clients/pirkpatogiai/brand.md` · faktai: `_facts.md`

Bendra: **15 laiškų, 6 srautai** (welcome 3 iš Luko GitHub repo, krepšelis 3, atsiskaitymas 2, naršymas 2, po pirkimo 3, sugrąžinimas 2). Be hero paveikslų (Luko sprendimas 09-09). Visos prekės - per Omnisend natūralius dinaminius blokus:
krepšelio prekės (2 stulpeliai) ir **8x2 recommender'iai** (populiariausios / paskutinės peržiūrėtos, 4 eilutės x 2). Copy per `lt_copy.py` (`_gen_copy.py` → `_copy/*.txt`).
Dizainas atkartoja svetainę: lime header `#c9e165` su tikru logotipu, tamsi meniu juosta `#2f2f2f` su lime nuorodomis, Poppins + Karla, šviesus footer `#f5f5f5`.
**2026-09-11 (Lukas):** visi akcentai (mygtukai, žingsnių apskritimai, juostos, paneliai) perdažyti iš alyvuogių `#b8ce5c` (atrodė rusva šalia welcome) į welcome flow žalią `#c9e165`; `_build.py LIME = LIME2 = #c9e165`, švelni panelių spalva `#f7fae6`. 12 gyvų Omnisend laiškų atnaujinti vietoje per `_recolor_omnisend.py put` (PUT /email-content, tie patys template/automation ID, welcome neliestas). Be nuolaidų kodų, be atsiliepimų (svetainėje jų nėra), visi faktai iš pirkpatogiai.lt.

## Laiškų struktūros (visos skirtingos)

| # | Laiškas | Struktūra |
|---|---|---|
| cart-01 | Krepšelis laukia | intro → **krepšelio blokas** → CTA → pastaba → pasitikėjimo 2x2 → P.S. |
| cart-02 | Kaip vyksta užsakymas | intro → **krepšelio blokas** → 3 žingsnių timeline (patvirtinimas / siuntimas / kurjeris 6-9 d.d.) → CTA → **populiariausios 8x2** |
| cart-03 | Paskutinis priminimas | tamsus antraštės blokas → **krepšelio blokas** → 3 privalumų juosta → CTA → D.U.K. (pristatymas / atsiskaitymas / grąžinimas) |
| checkout-01 | Liko vienas žingsnis | progreso juosta (krepšelis ✓ duomenys ✓ apmokėjimas) → **užsakymo blokas** → CTA + Paysera eilutė → saugumo panelė → kontaktų kortelė → pasitikėjimo 2x2 |
| checkout-02 | Galime padėti | 3 pagalbos kortelės (mokėjimas nepavyko / pristatymas / pakeisti) → CTA → **užsakymo blokas** → **populiariausios 8x2** → kontaktai |
| browse-01 | Peržiūrėtos prekės | intro → **peržiūrėtos prekės 8x2** (recentlyViewed, fallback popular) → lime CTA → 4 kategorijų kortelės 2x2 → P.S. |
| browse-02 | Kaip išsirinkti baldus | intro → **populiariausios 8x2** → 3 patarimai (matmenys / medžiaga ir apkrova / pristatymas ir grąžinimas) → grąžinimo panelė → CTA į parduotuvę → parašas |

## Flow 1 · Welcome (3) - Luko failai iš GitHub

Šaltinis: `elaiskai/pirkpatogiai-email-assets` (3 HTML + `omnisend/*.html` + `omnisend/styles.css`, LABAS10 -10 %, „tu" forma, hero per raw.githubusercontent.com). Lokali kopija `_welcome_raw/`, preview `01-welcome/`. Sukelta per API kaip Custom HTML blokas (`htmlCode` body + style) - tiksliai taip, kaip prašo repo `BRAND_NOTES.md`.

Trigger **Subscribed to marketing** (first subscription = true) · #1 iškart → +1 d. #2 → +2 d. #3 · Exit: placed order · Email tik subscribed.

| # | Delay | Failas | Subject |
|---|---|---|---|
| 1 | iškart | `01-welcome/01-labas-namai.html` | Labas! Tau – 10 % nuolaida su LABAS10 |
| 2 | +1 d. | `01-welcome/02-tavo-ritmui.html` | Erdvė, kuri tinka tavo kasdienybei |
| 3 | +2 d. | `01-welcome/03-issirink-patogiau.html` | Mažas pokytis namuose? Pradėk su LABAS10 |

Automatizacija `6aa18b226caa6c30ef40d5eb` (DISABLED) · template'ai `6aa18b211649cdadfc82c65f` · `6aa18b211649cdadfc82c664` · `6aa18b215d617daba136f618`. Prieš įjungiant: parduotuvėje turi veikti kodas **LABAS10 = 10 %** (BRAND_NOTES: minimali suma / išimtys / terminas nenurodyti), signup forma turi žadėti tą patį pasiūlymą.

## Flow 2 · Apleistas krepšelis (3)

Trigger **Added product to cart** · inactivity 1 val. · Exit: placed order / order fulfilled · Frequency 5 d. · Email: non-subscribed OK (transactional-type).

| # | Delay | Failas | Subject | Preheader |
|---|---|---|---|---|
| 1 | 1 val. | `02-cart/01-krepselis-laukia.html` | Jūsų prekės liko krepšelyje | Grįžkite į krepšelį ir užbaikite užsakymą, kai Jums patogu. |
| 2 | +24 val. | `02-cart/02-kaip-vyksta-uzsakymas.html` | Užsakymą užbaigsite vos per minutę | Saugiai atsiskaitykite, o prekes pristatysime per 6-9 darbo dienas. |
| 3 | +48 val. | `02-cart/03-paskutinis-priminimas.html` | Paskutinis priminimas apie Jūsų krepšelį | Jūsų krepšelis dar išsaugotas, o žemiau rasite atsakymus į dažnus klausimus. |

## Flow 3 · Apleistas atsiskaitymas (2)

Trigger **Started checkout** · inactivity 1 val. · Exit: placed order / order fulfilled · overlap: praleisti kontaktus, kurie šiuo metu krepšelio flow'e.

| # | Delay | Failas | Subject | Preheader |
|---|---|---|---|---|
| 1 | 1 val. | `03-checkout/01-liko-vienas-zingsnis.html` | Jūsų užsakymas beveik baigtas | Liko tik saugiai apmokėti užsakymą |
| 2 | +24 val. | `03-checkout/02-galime-padeti.html` | Ar galime padėti užbaigti užsakymą? | Jūsų užsakymas išsaugotas - atsakome į dažniausiai kylančius klausimus. |

## Flow 4 · Naršymo priminimas (2)

Trigger **Viewed product** (in stock) · Exit: added to cart / placed order · Frequency 4 d. · Email tik **subscribed**.

| # | Delay | Failas | Subject | Preheader |
|---|---|---|---|---|
| 1 | 4 val. | `04-browse/01-perziuretos-prekes.html` | Prekės, kurias neseniai žiūrėjote | Išsaugojome peržiūrėtas prekes, kad galėtumėte lengvai prie jų grįžti. |
| 2 | +2 d. | `04-browse/02-kaip-issirinkti.html` | Kaip išsirinkti baldus internetu | Trys dalykai, kuriuos verta patikrinti prieš užsakant baldus |

## Flow 5 · Po pirkimo (3)

Trigger **Placed order** · be exit · Frequency 30 d. Nedubliuoja OpenCart užsakymo patvirtinimo (tai padėka + kas toliau).

| # | Delay | Failas | Subject | Struktūra |
|---|---|---|---|---|
| 1 | 10 min. | `05-post-purchase/01-aciu-uz-uzsakyma.html` | Ačiū už Jūsų užsakymą | 3 žingsniai → sąskaitos panelė (per 3 d.d. nuo perdavimo kurjeriui) → „norite pakeisti" kontaktų kortelė → trust 2x2 → parašas |
| 2 | +12 d. | `05-post-purchase/02-ar-viskas-pavyko.html` | Ar viskas gerai su Jūsų užsakymu? | 3 situacijų kortelės → grąžinimo panelė → **populiariausios 8x2** → CTA |
| 3 | +9 d. (21 d.) | `05-post-purchase/03-jusu-nuomone.html` | Pasidalykite nuomone apie savo pirkinį | tamsus headline → lime CTA (mailto atsiliepimui) → dovanų kupono panelė → 4 kategorijų kortelės |

## Flow 6 · Sugrąžinimas (2)

Trigger **Placed order** · delay 90 d. · Exit: placed order · Frequency 60 d. · Email tik subscribed. Be nuolaidų kodų.

| # | Delay | Failas | Subject | Struktūra |
|---|---|---|---|---|
| 1 | 90 d. | `06-winback/01-seniai-nesimateme.html` | Seniai nesimatėme - kas naujo namams | **populiariausios 8x2** → specialių pasiūlymų panelė → CTA į /product/special → privalumų juosta |
| 2 | +14 d. | `06-winback/02-idejos-namams.html` | Namų kategorijos, kurių gal nematėte | 4 kategorijų kortelės (svetainė / miegamasis / prieškambaris / sodas) → **populiariausios 8x2** → kontaktų kortelė → CTA → P.S. su unsubscribe |

## ✅ Omnisend'e (sukelta per API 2026-09-09, visos DISABLED)

Paskyra nauja: 0 automatizacijų, **0 produktų, 0 segmentų** → OpenCart integracija dar neprijungta. Sender `Pirk Patogiai <noreply@pirkpatogiai.lt>` (vienintelis svetainės adresas, keisti UI jei Remigijus duos kitą). Omnisend prideda savo `badge` sekciją laiško gale (nemokamo plano ženkliukas).

| Flow | Automatizacija | Template'ai |
|---|---|---|
| 2 Apleistas krepšelis | `6aa175056caa6c30ef40d530` | `6aa175044a42732f6fd7bc47` · `6aa175045d617daba136b5e9` · `6aa17505adcc5181e4471c06` |
| 3 Apleistas atsiskaitymas | `6aa1750e086a0d661ef0ca65` | `6aa1750d5d617daba136b650` · `6aa1750dadcc5181e4471ca6` |
| 4 Naršymo priminimas | `6aa1750f086a0d661ef0ca69` | `6aa1750e4a42732f6fd7bc95` · `6aa1750fadcc5181e4471cf9` |
| 5 Po pirkimo | `6aa1758abc4dae701b25e132` | `6aa175894a42732f6fd7bcd6` · `6aa1758aadcc5181e4471dc2` · `6aa1758a5d617daba136b78d` |
| 6 Sugrąžinimas | `6aa1758c6caa6c30ef40d536` | `6aa1758b5d617daba136b7e4` · `6aa1758badcc5181e4471e15` |

Patikrinta per `_omnisend_verify.py`: kiekvienas laiškas = HTML | natūralus blokas (`product_cart_recovery` 4x2 arba `product_recommender` popular / recentlyViewed 4x2) | HTML. Checkout + browse turi overlap guard (praleisti kontaktus, kurie šiuo metu krepšelio flow'e). Key: `.omnisend_key` (gitignored).

## Kaip kelti į Omnisend

**Per API (rekomenduojama, kai bus key):** įdėti key į `clients/pirkpatogiai/automations/.omnisend_key` (arba env `OMNISEND_API_KEY_PIRKPATOGIAI`), tada:
```
python3 _omnisend_push_flows.py probe      # patikrina key, parodo esamas default automatizacijas
python3 _omnisend_push_flows.py cart       # sukuria 3 template'us + DISABLED automatizaciją, id -> _omnisend_ids.json
python3 _omnisend_push_flows.py checkout
python3 _omnisend_push_flows.py browse
```
Script'as HTML'ą pjauna ties `<!--SPLIT:cart|popular|viewed-->` ir įterpia natūralias sekcijas: `product_cart_recovery` (2 stulp., mygtukas „Grįžti į krepšelį" / „Užbaigti užsakymą"), `product_recommender` type=popular 4x2, type=recentlyViewed 4x2 (fallback popular). Tik GET + POST. Sender: `PP_SENDER_EMAIL` env (default info@pirkpatogiai.lt - **patvirtinti su Remigijum**, svetainėje rodomas tik noreply@).

**Rankiniu būdu (UI):** Automation → Email → Edit content → HTML Code block → įklijuoti failą; vietoje punktyrinio „Omnisend · …" bloko ištrinti tą `<table>` ir įdėti Omnisend bloką: *Abandoned Cart* / *Abandoned Checkout* / *Product recommender* (Best sellers arba Recently viewed), nustatyti 2 stulpelius, 8 prekes. Merge tag'ai CTA: `{{abandonedCheckoutUrl}}` (cart + checkout), `{{lastViewedProductUrl}}` (browse-01).

## Prieš įjungiant

- [ ] Remigijus patvirtina laiškus (preview nuoroda viršuje) + sender'io el. paštą ir vardą
- [ ] Omnisend paskyra + API key; OpenCart ↔ Omnisend integracija siunčia **cart / checkout / viewed product** eventus (be jų flow'ai neužsives) - patikrinti per `probe` ir Omnisend Store connection
- [ ] Sender domeno autentifikacija (SPF/DKIM) pirkpatogiai.lt
- [ ] Test send kiekvieno laiško (patikrinti, kaip natūralūs blokai atrodo su realiomis prekėmis ir kainomis)
- [ ] Išjungti Omnisend default LT abandoned cart / browse flow'us, kad nesidubliuotų
- [x] cart-01 P.S. „atsakykite į šį laišką" ištrintas (Lukas 09-09), vietoje jo kontaktų eilutė
- [ ] **Prijungti OpenCart → Omnisend** (produktai, cart/checkout/viewed/order eventai) - be to nė vienas flow neužsives, o 8x2 blokai bus tušti
- [ ] Post-03 CTA = `mailto:noreply@pirkpatogiai.lt` (atsiliepimai renkami el. paštu, kaip svetainėje) - jei noreply nepriima laiškų, pakeisti adresą `_build.py FEEDBACK_MAILTO`
- [ ] Footer'yje yra `[[account.address]]` + `[[unsubscribe_link]]` (kaip Bakli v2). Jei Omnisend prideda ir savo footer'į, HTML footer'io apatines 2 eilutes galima išimti (`_build.py footer()`)

## Failai

`_build.py` (HTML iš `_copy/`), `_gen_copy.py` (copy per lt_copy), `_omnisend_push_flows.py` (API push), `_push.py` (jsDelivr/Pages), `_index.py` (index.html), `_screenshot.py` (QA png į `_render/`), `_facts.md`, `logo-pirkpatogiai.png`.
