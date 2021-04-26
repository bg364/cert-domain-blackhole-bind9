
# Ostrzeżenie przed niebezpiecznymi stronami
Prosty skrypt napisany w bashu do automatycznego importu listy domen phishingowych publikowanych przez CERT do serwera nazw domenowych BIND9.

Informacje na temat listy można znaleźć tu:
https://lista.cert.pl/
https://www.cert.pl/posts/2020/03/ostrzezenia_phishing/

# Pierwsza instalacja
Zakładam, że posiadamy aktualnie zainstalowany serwer BIND9 (lub kompatybilny), oraz, że jego konfiguracja znajduje się w folderze **/etc/named**

Klonujemy repozytorium do dowolnego katalogu:

    git clone https://github.com/bg364/cert-domain-blackhole-bind9.git

Przechodzimy do katalogu z projektem:

    cd cert-domain-blackhole-bind9

Kopiujemy plik **cert-blackhole.zone** do katalogu **/etc/named**

    cp cert-blackhole.zone /etc/named
Nadajemy uprawnienia uruchamiania do pliku **update_cert_domains**

    chmod +x update_cert_domains
po czym go uruchamiamy

    ./update_cert_domains

Przechodzimy do pliku konfiguracyjnego serwera BIND9 i na jego końcu dodajemy:

    include "/etc/named/cert-blackhole.conf";


Po czym przeładowujemy usługę:

    service named restart


Opcjonalnie można również dodać powyższy skrypt do crontaba.
