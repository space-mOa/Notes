# OAuth2 🔐

K poskytnutí bezpečné __autentizace__ a __autorizace__. Služby např. twitter -> poskytují možnost sdílet uživatelská data a identity -> aniž by musely prozrazovat heslo někomu
dalšímu (např. mě, heslo zná jen twitter). 


## Pojmy

#### Third party application: client
_aplikace třetí strany_
- App, která se snaží získat přístup do učtu uživatele. Potřebuje povolení. 
#### The API: "Resource Server"
- Server s informacemi o uživateli
#### The authorization server
- Zprostředkovává rozhraní
- Pomocí něhoko uživatel potvrdí nebo zamítné
- Někdy je stejné s API serverem
#### The User: "resource owner"
- uživatel který dává povolení o přístupu k části jeho dat

## Vytvoření App

- nejdříve je nutné vyplnit registraci aplikace u služby např. Twitter
- většinou registrujeme informace o např. názvu aplikace a redirect uri

	#### Redirect URI - _pro mého bota to nepotřebuju myslím_
	_přesměrovací uri_
	- přesměruje je na registrované uri
	- server přesměruje jen na registrované uri a musí mít https:\\  
---

## Resources
[Oauth-webguide-simplified](https://aaronparecki.com/oauth-2-simplified/#roles)
