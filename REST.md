# REST: representional state transfer

- trasnfer data 
- alternativa k tradiční webové stránka

KLIENT --Request--> SERVER

SERVER --Response--> KLIENT

- např. když chceme jenom vyměnit data 
- Statless Backend: neukládáme session klienta
- Nepoužívá html


### RESTFUL SERVER API (Má url)
- ```/user```
    * ```GET```   
    * ```POST```
    * ```DELETE```
- ```/posts```
    * ```GET```   
    * ```POST```
    * ```DELETE```

---Response---> KLIENT ---Request("AJAX")---> SERVER REST

- data mohou být např. v JSON, XML, URLEncoded
- neměl bych brát ohlend na UI v RESTful API
- Cacheable: jestli mohou být nebo ne (*dovolit browseru cacheovat data*)
- Layered System -> klient vidí jen jednu vrstvu
- jednotné rozhraní: Resources jsou definované v Requestu a přenášena datajsou oddělené od DB schématu dat, zpráva s popisem dat
- nemusí to být jen data, ale i kód, které data může execute 
