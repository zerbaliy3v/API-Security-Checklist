[English](./README.md) | [繁中版](./README-tw.md) | [简中版](./README-zh.md) | [العربية](./README-ar.md) | [Azərbaycan](./README-az.md) | [বাংলা](./README-bn.md) | [Čeština](./README-cs.md) | [Deutsch](./README-de.md) | [Ελληνικά](./README-el.md) | [Español](./README-es.md) | [فارسی](./README-fa.md) | [Français](./README-fr.md) | [हिंदी](./README-hi.md) | [Indonesia](./README-id.md) | [Italiano](./README-it.md) | [日本語](./README-ja.md) | [한국어](./README-ko.md) | [ພາສາລາວ](./README-lo.md) | [Македонски](./README-mk.md) | [Монгол](./README-mn.md) | [Nederlands](./README-nl.md) | [Polski](./README-pl.md) | [Português (Brasil)](./README-pt_BR.md) | [Русский](./README-ru.md) | [ไทย](./README-th.md) | [Türkçe](./README-tr.md) | [Українська](./README-uk.md) | [Tiếng Việt](./README-vi.md)

# API സുരക്ഷാ ചെക്ക്‌ലിസ്റ്റ്

നിങ്ങളുടെ API ഡിസൈൻ ചെയ്യുമ്പോഴും ടെസ്റ്റ് ചെയ്യുമ്പോഴും റിലീസ് ചെയ്യുമ്പോഴും പാലിക്കേണ്ട ഏറ്റവും പ്രധാനപ്പെട്ട സുരക്ഷാ പ്രതിരോധ നടപടികളുടെ ചെക്ക്‌ലിസ്റ്റ്.

---

## ഒതെന്റിക്കേഷൻ

- [ ] `Basic Auth` ഉപയോഗിക്കരുത്. പകരം സ്റ്റാൻഡേർഡ് ഓതെന്റിക്കേഷൻ ഉപയോഗിക്കുക (e.g. [JWT](https://jwt.io/), [OAuth](https://oauth.net/)).
- [ ] `Authentication`, `token generation`, `password storage` എന്നിവയിൽ മുമ്പ് സൃഷ്ടിച്ച അടിസ്ഥാന രീതിയുടെ ആവർത്തനം ഉണ്ടാകരുത്. മാനദണ്ഡങ്ങൾ പാലിക്കുക.
- [ ] ലോഗിനിൽ `Max Retry` യും ജയിൽ ഫീച്ചേഴ്സും ഉപയോഗിക്കുക.
- [ ] എല്ലാ സെൻസിറ്റീവ് ഡാറ്റയിലും എൻക്രിപ്ഷൻ ഉപയോഗിക്കുക.

### JWT (JSON വെബ് ടോക്കൺ)

- [ ] ഒരു റാൻഡം കോംപ്ലിക്കേറ്റഡ് കീ ( `JWT Secret`) ഉപയോഗിച്ച് ടോക്കണിനെ ബ്രൂട്ട് ഫോഴ്‌സ് ചെയ്യുന്നത് ബുദ്ധിമുട്ടുള്ളതാക്കാം.
- [ ] ഹെയ്ഡറിൽ നിന്ന് അൽഗോരിതം വേര്തിരിച്ചെടുക്കരുത്. അൽഗോരിതത്തെ ബേക്ക്എന്റിൽ തന്നെ നിലനിർത്തുക (`HS256` അല്ലെങ്കിൽ `RS256`).
- [ ] ടോക്കൺ കാലഹരണപ്പെടൽ (` TTL`, `RTTL`) കഴിയുന്നത്ര ചെറുതാക്കുക.
- [ ] സെൻസിറ്റീവ് ഡാറ്റ JWT പേലോഡിൽ സൂക്ഷിക്കരുത്, അത് [എളുപ്പത്തിൽ](https://jwt.io/#debugger-io) ഡീകോഡ് ചെയ്യാം .
- [ ] വളരെയധികം ഡാറ്റ സൂക്ഷിക്കുന്നത് ഒഴിവാക്കുക. JWT സാധാരണയായി headerകളിൽ പങ്കിടുന്നു, അവയ്‌ക്ക് വലുപ്പ പരിധിയുണ്ട്.

## ആക്സസ്

- [ ] DDoS / ബ്രൂട്ട്-ഫോഴ്സ് ആക്രമണങ്ങൾ ഒഴിവാക്കാൻ റിക്വറ്റുകൾ (ത്രോട്ടിലിംഗ്) പരിമിതപ്പെടുത്തുക.
- [ ] MITM (മാൻ ഇൻ ദ മിഡിൽ അറ്റാക്ക്) ഒഴിവാക്കാൻ സെർവർ സൈഡിൽ HTTPS ഉപയോഗിക്കുക.
- [ ] SSL സ്ട്രിപ്പ് ആക്രമണം ഒഴിവാക്കാൻ SSL-നൊപ്പം `HSTS` ഹെഡർ ഉപയോഗിക്കുക.
- [ ] ഡയറക്ടറി ലിസ്റ്റിംഗുകൾ ഓഫാക്കുക.
- [ ] സ്വകാര്യ API-കൾക്കായി, വൈറ്റ്‌ലിസ്റ്റ് ചെയ്‌ത IP-കൾ/ഹോസ്റ്റുകളിൽ നിന്ന് മാത്രം ആക്‌സസ് അനുവദിക്കുക.

## Authorization

### OAuth

- [ ] വൈറ്റ്‌ലിസ്റ്റ് ചെയ്‌ത URL-കൾ മാത്രം അനുവദിക്കുന്നതിന് സെർവർ സൈഡിൽ എല്ലായ്‌പ്പോഴും `redirect_uri` സാധൂകരിക്കുക.
- [ ] എപ്പോഴും ടോക്കണുകൾ കൈമാറാതെ പകരം കോഡുകൾ കൈമാറാൻ ശ്രമിക്കുക (`response_type=token` അനുവദിക്കരുത്).
- [ ] `state` പരാമീറ്ററിനോടൊപ്പം ഒരു റാൻഡം ഹാഷ് ഉപയോഗിച്ച് OAuth ഓതെന്റിക്കേഷൻ പ്രോസസ്സിലെ `CSRF` തടയാനാവും.
- [ ] ഓരോ ആപ്ലിക്കേഷനും ഡിഫോൾട്ട് സ്കോപ്പ് നിർവചിക്കുകയും സ്കോപ്പ് പാരാമീറ്ററുകൾ സാധൂകരിക്കുകയും ചെയ്യുക.

## ഇൻപുട്ട്

- [ ] പ്രവർത്തനത്തിനനുസരിച്ച് ശരിയായ HTTP രീതി ഉപയോഗിക്കുക: `GET (read)`, `POST (create)`, `PUT/PATCH (replace/update)`, and `DELETE (to delete a record)`, അഭ്യർത്ഥിച്ച ഉറവിടത്തിന് അഭ്യർത്ഥിച്ച രീതി അനുയോജ്യമല്ലെങ്കിൽ `405 Method Not Allowed` എന്ന് പ്രതികരിക്കുക.
- [ ] Accept ഹെഡ്‍ർ (കണ്ടെന്റ് നെഗോഷിയേഷൻ) അവശ്യപെടുന്നതിനനുസരിച്ചു `content-type` വാലിഡേറ്റ് ചെയ്യുകയും സപ്പോർട്ട് ചെയ്യുന്ന ഫോർമാറ്റുകൾ മാത്രം അനുവദിക്കുകയും (ഉദാ. `application/xml`, `application/json`, മുതലായവ) പൊരുത്തപ്പെടുന്നില്ലെങ്കിൽ `406 Not Acceptable` എന്ന റെസ്പോൻഡ്‌സ് ഉപയോഗിച്ച് പ്രതികരിക്കുകയും ചെയ്യുക.
- [ ] പോസ്റ്റ് ചെയ്‌ത ടാറ്റായുടെ `content-type` നിങ്ങൾ അനുവദിക്കുന്നതതിനനുസരിച് വാലിഡേറ്റ് ചെയ്യുക. (ഉദാ: `application/x-www-form-urlencoded`, `multipart/form-data`, `application/json`, മുതലായവ).
- [ ] പൊതുവായ വൾനറബിലിറ്റികൾ ഒഴിവാക്കാൻ യൂസർ ഇൻപുട്ട് സാധൂകരിക്കുക (ഉദാ: `XSS`, `SQL-ഇൻജെക്ഷൻ`, `റിമോട്ട് കോഡ് എക്സിക്യൂഷൻ`, മുതലായവ).
- [ ] സെർവർ സൈഡ് എൻക്രിപ്ഷൻ മാത്രം ഉപയോഗിക്കുക.
- [ ] സെർവർ സൈഡ് എൻക്രിപ്ഷൻ മാത്രം ഉപയോഗിക്കുക.
- [ ] കാഷിംഗ്, നിരക്ക് പരിധി നയങ്ങൾ (ഉദാ. `Quota`, `Spike Arrest`, `Concurrent Rate Limit`) എന്നിവ പ്രവർത്തനക്ഷമമാക്കുന്നതിനും API-കളുടെ ഉറവിടങ്ങൾ ചലനാത്മകമായി വിന്യസിക്കുന്നതിനും ഒരു API ഗേറ്റ്‌വേ സേവനം ഉപയോഗിക്കുക.

## പ്രോസസ്സിംഗ്

- [ ] തകർന്ന ഓതെന്റിക്കേഷൻ പ്രക്രിയ ഒഴിവാക്കാൻ എല്ലാ എൻഡ് പോയിന്റുകളും ഓതെന്റിക്കേഷൻന് പിന്നിൽ പരിരക്ഷിച്ചിട്ടുണ്ടോയെന്ന് പരിശോധിക്കുക.
- [ ] ഉപയോക്താവിന്റെ സ്വന്തം റിസോഴ്സ് ഐഡി ഒഴിവാക്കണം. `/me/orders` പകരം `/user/654321/orders` ഉപയോഗിക്കുക.
- [ ] ഐഡികൾ ഓട്ടോ-ഇൻക്രിമെന്റ് ചെയ്യരുത്. പകരം `UUID` ഉപയോഗിക്കുക.
- [ ] നിങ്ങൾ XML ഫയലുകൾ പാഴ്‌സ് ചെയ്യുകയാണെങ്കിൽ, `XXE` (XML ബാഹ്യ എന്റിറ്റി ആക്രമണം) ഒഴിവാക്കുവാൻ എന്റിറ്റി പാഴ്‌സിംഗ് പ്രവർത്തനക്ഷമമാക്കിയിട്ടില്ലെന്ന് ഉറപ്പാക്കുക.
- [ ] നിങ്ങൾ XML ഫയലുകൾ പാഴ്‌സ് ചെയ്യുകയാണെങ്കിൽ, `Billion Laughs/XML bomb` വഴി എക്‌സ്‌പോണൻഷ്യൽ എന്റിറ്റി എക്സ്പാൻഷൻ അറ്റാക്ക് ഒഴിവാക്കാൻ എന്റിറ്റി വിപുലീകരണം പ്രവർത്തനക്ഷമമാക്കിയിട്ടില്ലെന്ന് ഉറപ്പാക്കുക.
- [ ] ഫയൽ അപ്‌ലോഡുകൾക്കായി ഒരു CDN ഉപയോഗിക്കുക.
- [ ] നിങ്ങൾ വലിയ അളവിലുള്ള ഡാറ്റയാണ് കൈകാര്യം ചെയ്യുന്നതെങ്കിൽ, HTTP തടയൽ ഒഴിവാക്കുന്നതിന് പശ്ചാത്തലത്തിൽ കഴിയുന്നത്ര പ്രോസസ്സ് ചെയ്യാനും പ്രതികരണം വേഗത്തിൽ തിരികെ നൽകാനും വർക്കേഴ്സും ക്യൂകളും ഉപയോഗിക്കുക.
- [ ] ഡീബഗ് മോഡ് ഓഫ് ചെയ്യാൻ മറക്കരുത്.
- [ ] ലഭ്യമാകുമ്പോൾ എക്സിക്യൂട്ടബിൾ അല്ലാത്ത stackകൾ ഉപയോഗിക്കുക.

## ഔട്ട്പുട്ട്

- [ ] `X-Content-Type-Options: nosniff` ഹെഡ്‍ർ അയയ്ക്കുക.
- [ ] `X-Frame-Options: deny` ഹെഡ്‍ർ അയയ്ക്കുക.
- [ ] `Content-Security-Policy: default-src 'none'` ഹെഡ്‍ർ അയയ്ക്കുക.
- [ ] ഫിംഗർപ്രിന്റിങ് ഹെൽഡറുകൾ നീക്കം ചെയ്യുക - `X-Powered-By`, `Server`, `X-AspNet-Version` മുതലായവ.
- [ ] `content-type` നെ നിങ്ങളുടെ പ്രതികരണത്തിനായി നിർബന്ധിക്കുക. നിങ്ങളുടെ പ്രതികരണം `application/json` ആണെങ്കിൽ, നിങ്ങളുടെ `content-type` പ്രതികരണവും `application/json` ആയിരിക്കും.
- [ ] `Credentials`, `passwords` അല്ലെങ്കിൽ `security tokens` പോലുള്ള സെൻസിറ്റീവ് ഡാറ്റ നൽകരുത്.
- [ ] പൂർത്തിയാക്കിയ പ്രവർത്തനത്തിനനുസരിച്ച് ശരിയായ സ്റ്റാറ്റസ് കോഡ് തിരികെ നൽകുക. (ഉദാ: `200 OK`, `400 Bad Request`, `401 Unauthorized`, `405 Method Not Allowed`, മുതലായവ).

## CI & CD

- [ ] unit/integration tests കോവേജ് ഉപയോഗിച്ച് നിങ്ങളുടെ ഡിസൈനും ഇമ്പലമെന്റാഷനും ഔഡിഡ് ചെയ്യുക.
- [ ] ഒരു കോഡ് റിവ്യൂ പ്രക്രിയ ഉപയോഗിക്കുക, സ്വയം അംഗീകാരം അവഗണിക്കുക.
- [ ] വെണ്ടർ ലൈബ്രറികളും മറ്റ് ഡിപൻഡൻസികളും ഉൾപ്പെടെ ഉൽപ്പാദനത്തിലേക്ക് നീങ്ങുന്നതിന് മുമ്പ് നിങ്ങളുടെ സേവനങ്ങളുടെ എല്ലാ ഘടകങ്ങളും എവി സോഫ്‌റ്റ്‌വെയർ സ്ഥിരമായി സ്കാൻ ചെയ്തിട്ടുണ്ടെന്ന് ഉറപ്പാക്കുക.
- [ ] നിങ്ങളുടെ കോഡിൽ സുരക്ഷാ പരിശോധനകൾ (സ്റ്റാറ്റിക്/ഡൈനാമിക് അനാലിസിസ്) തുടർച്ചയായി പ്രവർത്തിപ്പിക്കുക.
- [ ] അറിയപ്പെടുന്ന കേടുപാടുകൾക്കായി നിങ്ങളുടെ ഡിപൻഡൻസികൾ (സോഫ്‌റ്റ്‌വെയറും ഒഎസും) പരിശോധിക്കുക.
- [ ] ഡിപ്ലോയ്‌മെന്റിനായി ഒരു റോൾബാക്ക് പരിഹാരം രൂപകൽപ്പന ചെയ്യുക.

## Monitoring

- [ ] എല്ലാ സേവനങ്ങൾക്കും ഘടകങ്ങൾക്കുമായി കേന്ദ്രീകൃത ലോഗിനുകൾ ഉപയോഗിക്കുക.
- [ ] എല്ലാ ട്രാഫിക്കും എററുകളും റിക്യുസ്റ്റുകളും റെസ്പോണ്ട്സുകളും നിരീക്ഷിക്കാൻ ഏജന്റ്സ് ഉപയോഗിക്കുക.
- [ ] SMS, Slack, Email, Telegram, Kibana, Cloudwatch മുതലായവയ്‌ക്കായി അലേർട്ടുകൾ ഉപയോഗിക്കുക.
- [ ] ക്രെഡിറ്റ് കാർഡുകൾ, പാസ്‌വേഡുകൾ, പിന്നുകൾ മുതലായവ പോലുള്ള സെൻസിറ്റീവ് ഡാറ്റയൊന്നും നിങ്ങൾ ലോഗ് ചെയ്യുന്നില്ലെന്ന് ഉറപ്പാക്കുക.
- [ ] നിങ്ങളുടെ API റിക്യുസ്റ്റുകളും ഇൻസ്റ്റൻസുകളും നിരീക്ഷിക്കാൻ ഒരു IDS കൂടാതെ/അല്ലെങ്കിൽ IPS സിസ്റ്റം ഉപയോഗിക്കുക.

---

## ഇതും കാണുക:

- [yosriady/api-development-tools](https://github.com/yosriady/api-development-tools) - RESTful HTTP+JSON API-കൾ നിർമ്മിക്കുന്നതിനുള്ള ഉപയോഗപ്രദമായ വിഭവങ്ങളുടെ ഒരു ശേഖരം.

---

# സംഭാവന

ഈ ശേഖരം ഫോർക്ക് ചെയ്തും ചില മാറ്റങ്ങൾ വരുത്തിയും പുൾ അഭ്യർത്ഥനകൾ സമർപ്പിച്ചും സംഭാവന ചെയ്യാൻ മടിക്കേണ്ടതില്ല. എന്തെങ്കിലും ചോദ്യങ്ങൾക്ക് ഞങ്ങൾക്ക് ഒരു ഇമെയിൽ അയയ്ക്കുക `team@shieldfy.io`.
