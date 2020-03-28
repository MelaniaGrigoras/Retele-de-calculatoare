# Tema 2

## Exerciții HTTP/S
1. Cloudflare are un serviciu DoH care ruleaza pe IP-ul [1.1.1.1](https://blog.cloudflare.com/announcing-1111/). Urmăriți [aici documentația](https://developers.cloudflare.com/1.1.1.1/dns-over-https/json-format/) pentru request-uri de tip GET către cloudflare-dns și scrieți o funcție care returnează adresa IP pentru un nume dat ca parametru. Indicații: setați header-ul cu {'accept': 'application/dns-json'}.

  ![alt_text](https://github.com/nlp-unibuc/tema-2-MelaniaGrigoras/blob/master/Screenshots/HTTPex1.png)

---

2. Executati pe containerul `rt1` scriptul 'simple_flask.py' care deserveste API HTTP pentru GET si POST. Daca accesati in browser [http://localhost:8001](http://localhost:8001) ce observati?

  ![alt_text](https://github.com/nlp-unibuc/tema-2-MelaniaGrigoras/blob/master/Screenshots/HTTPex2_1.png)
  
  ![alt_text](https://github.com/nlp-unibuc/tema-2-MelaniaGrigoras/blob/master/Screenshots/HTTPex2_2.png)
  
---

3. Conectați-vă la containerul `docker-compose exec rt2 bash`. Testati conexiunea catre API-ul care ruleaza pe rt1 folosind curl: `curl -X POST http://rt1:8001/post  -d '{"value": 10}' -H 'Content-Type: application/json'`. Scrieti o metoda POST care ridică la pătrat un numărul definit în `value`. Apelați-o din cod folosind python requests.

  ![alt_text](https://github.com/nlp-unibuc/tema-2-MelaniaGrigoras/blob/master/Screenshots/HTTPex3_1.png)
  
  ![alt_text](https://github.com/nlp-unibuc/tema-2-MelaniaGrigoras/blob/master/Screenshots/HTTPex3_2.png)

---

4. Urmăriți alte exemple de request-uri pe [HTTPbin](http://httpbin.org/)
```
Am aflat de metodele HTTP, GET, POST, PUT, DELETE.
```

---


## Exerciții UDP
1. Executați serverul apoi clientul fie într-un container de docker fie pe calculatorul vostru personal: `python3 udp_server.py` și `python3 udp_client.py "mesaj de trimis"`.

Printscreen cu rezultatul:

  ![alt text](https://github.com/nlp-unibuc/tema-2-MelaniaGrigoras/blob/master/Screenshots/UDPex1_1.png)

  ![alt text](https://github.com/nlp-unibuc/tema-2-MelaniaGrigoras/blob/master/Screenshots/UDPex1_2.png)
---

2. Modificați adresa de pornire a serverului din 'localhost' în IP-ul rezervat descris mai sus cu scopul de a permite serverului să comunice pe rețea cu containere din exterior. 

  ![alt text](https://github.com/nlp-unibuc/tema-2-MelaniaGrigoras/blob/master/Screenshots/UDPex2.png)

---

3. Porniți un terminal în directorul capitolul2 și atașați-vă la containerul rt1: `docker-compose exec rt1 bash`. Pe rt1 folositi calea relativă montată în directorul elocal pentru a porni serverul: `python3 /elocal/src/udp_server.py`. 

  ![alt text](https://github.com/nlp-unibuc/tema-2-MelaniaGrigoras/blob/master/Screenshots/UDPex3.png)

---

4. Modificați udp_client.py ca el să se conecteze la adresa serverului, nu la 'localhost'. Sfaturi: puteți înlocui localhost cu adresa IP a containerului rt1 sau chiar cu numele 'rt1'.

  ![alt text](https://github.com/nlp-unibuc/tema-2-MelaniaGrigoras/blob/master/Screenshots/UDPex4.png)

---

5. Porniți un al doilea terminal în directorul capitolul2 și rulați clientul în containerul rt2 pentru a trimite un mesaj serverului:  `docker-compose exec rt2 bash -c "python3 /elocal/src/udp_client.py salut"`

  ![alt text](https://github.com/nlp-unibuc/tema-2-MelaniaGrigoras/blob/master/Screenshots/UDPex5_1.png)

  ![alt text](https://github.com/nlp-unibuc/tema-2-MelaniaGrigoras/blob/master/Screenshots/UDPex5_2.png)
---

6. Deschideți un al treilea terminal și atașați-vă containerului rt1: `docker-compose exec rt1 bash`. Utilizați `tcpdump -nvvX -i any udp port 10000` pentru a scana mesajele UDP care circulă pe portul 10000. Apoi apelați clientul pentru a genera trafic.

  ![alt text](https://github.com/nlp-unibuc/tema-2-MelaniaGrigoras/blob/master/Screenshots/UDPex6.png)

---

7. Containerul rt1 este definit în [docker-compose.yml](https://github.com/senisioi/computer-networks/blob/2020/capitolul2/docker-compose.yml) cu redirecționare pentru portul 8001. Modificați serverul și clientul în așa fel încât să îl puteți executa pe containerul rt1 și să puteți să vă conectați la el de pe calculatorul vostru sau de pe rețeaua pe care se află calculatorul vostru.

  ![alt text](https://github.com/nlp-unibuc/tema-2-MelaniaGrigoras/blob/master/Screenshots/UDPex7.png)

---


## Exerciții TCP

1. Executați serverul apoi clientul fie într-un container de docker fie pe calculatorul vostru personal: `python3 tcp_server.py` și `python3 tcp_client.py "mesaj de trimis"`.
```
A mers la UDP, aici nu mai e necesar.
```
---

2. Modificați adresa de pornire a serverului din 'localhost' în IP-ul rezervat '0.0.0.0' cu scopul de a permite serverului să comunice pe rețea cu containere din exterior. Modificați tcp_client.py ca el să se conecteze la adresa serverului, nu la 'localhost'. Pentru client, puteți înlocui localhost cu adresa IP a containerului rt1 sau chiar cu numele 'rt1'.
```
A mers la UDP, aici nu mai e necesar.
```

---

3. Într-un terminal, în containerul rt1 rulați serverul: `docker-compose exec rt1 bash -c "python3 /elocal/src/tcp_server.py"`. 
```
A mers la UDP, aici nu mai e necesar.
```

---

4. Într-un alt terminal, în containerul rt2 rulați clientul: `docker-compose exec rt1 bash -c "python3 /elocal/src/tcp_client.py TCP_MESAJ"`

Printscreen cu rezultatul:

  ![alt_text](https://github.com/nlp-unibuc/tema-2-MelaniaGrigoras/blob/master/Screenshots/TCPex4_1.png)

  ![alt_text](https://github.com/nlp-unibuc/tema-2-MelaniaGrigoras/blob/master/Screenshots/TCPex4_2.png)

---

5. Mai jos sunt explicați pașii din 3-way handshake captați de tcpdump și trimiterea unui singur byte de la client la server. Salvați un exemplu de tcpdump asemănător care conține și partea de [finalizare a conexiunii TCP](http://www.tcpipguide.com/free/t_TCPConnectionTermination-2.htm). Sfat: Modificați clientul să trimită un singur byte fără să facă recv. Modificați serverul să citească doar un singur byte cu recv(1) și să nu facă send. Reporniți serverul din rt1. Deschideți un al treilea terminal, tot în capitolul2 și rulați tcpdump: `docker-compose exec rt1 bash -c "tcpdump -Snnt tcp"` pentru a porni tcpdump pe rt1. 
  
  ![alt_text](https://github.com/nlp-unibuc/tema-2-MelaniaGrigoras/blob/master/Screenshots/TCPex5.png)
  
## 3-way handshake

# SYN:
Clientul apelează funcția connect(('172.9.0.1', 10000)) iar mesajul din spate arată așa:

```
    IP 172.9.0.2.38694 > 172.9.0.1.10000: Flags [S], seq 3216038318, win 64240, options [mss 1460,sackOK,TS val 677953593 ecr 0,nop,wscale 7], length 0

```

Flags [S] - cerere de sincronizare de la adresa 172.9.0.2 cu portul 38694 către adresa 172.9.0.1.10000 cu portul 10000
seq 3216038318 - primul sequence nr pe care îl setează clientul în mod aleatoriu
win 64240 - Window Size inițial.
options [mss 1460,sackOK,TS val 677953593 ecr 0,nop,wscale 7] - reprezintă Opțiuni de TCP. Cele din tcpdump în ordinea asta sunt: Maximum Segment Size (mss), Selective Acknowledgement, Timestamps (pentru round-trip-time), NOP (no option pentru separare între opțiuni) și Window Scaling.
length 0 - mesajul SYN nu are payload, conține doar headerul TCP

# SYN-ACK:
În acest punct lucrurile se întâmplă undeva în interiorul funcției accept din server la care nu avem acces. Serverul răspunde prin SYN-ACK:

```
    IP 172.9.0.1.10000 > 172.9.0.2.38694: Flags [S.], seq 15501656, ack 3216038319, win 65160, options [mss 1460,sackOK,TS val 135589725 ecr 677953593,nop,wscale 7], length 0

```
Flags [S.] - . (punct) reprezintă flag de Acknowledgement din partea serverului (172.9.0.1.10000) că a primit pachetul și returnează și un Acknowledgement number: ack 3216038319 care reprezintă Sequence number trimis de client + 1 (vezi mai sus la SYN).
Flags [S.] - în același timp, serverul trimite și el un flag de SYN și propriul Sequence number: seq 15501656
optiunile sunt la fel ca înainte și length 0, mesajul este compus doar din header, fără payload

# ACK:
După primirea cererii de sincronizare a serverului, clientul confirmă primirea, lucru care se execută în spatele funcției connect:

```
   IP 172.9.0.2.38694 > 172.9.0.1.10000: Flags [.], ack 15501657, win 502, options [nop,nop,TS val 677953593 ecr 135589725], length 0

```

Flags [.] - . (punct) este pus ca flack de Ack și se transmite Ack Number ca fiind seq number trimis de server + 1: ack 15501657
length 0, din nou, mesajul este fără payload, doar cu header

# PSH:
La trimiterea unui mesaj, se folosește flag-ul push (PSH) și intervalul de secventă de dimensiune 1:

```
   IP 172.9.0.2.38694 > 172.9.0.1.10000: Flags [P.], seq 3216038319:3216038320, ack 15501657, win 502, options [nop,nop,TS val 677956599 ecr 135589725], length 1

```

Flags [P.] - avem P și . (punct) care reprezintă PUSH de mesaj nou și Ack ultimului mesaj
seq 3216038319:3216038320 - se trimite o singură literă (un byte) iar numărul de secvență indică acest fapt
ack 15501657 - la orice mesaj, se confirmă prin trimiterea de Ack a ultimului mesaj primit, in acest caz se re-confirmă SYN-ACK-ul de la server
length 1 - se trimite un byte în payload

# ACK:
Serverul dacă primește mesaju, trimite automat un mesaj cu flag-ul ACK și Ack Nr numărul de octeți primiți.

```
    IP 172.9.0.1.10000 > 172.9.0.2.38694: Flags [.], ack 3216038320, win 510, options [nop,nop,TS val 135592731 ecr 677956599], length 0
    
```

Flags [.] - flag de Ack
ack 3216038320 - arată că am primit octeți pana la 3216038319, aștept octeți de la Seq Nr 3216038320
length 0 - un mesaj de confirmare nu are payload
