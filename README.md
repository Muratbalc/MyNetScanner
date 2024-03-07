Açıklamalar ile python NetScanner

# Ağ Tarama Aracı Açıklaması

## Gerekli Kütüphaneleri İçe Aktarma:

```python
import scapy.all as scapy
import optparse

#Bu satırlar, Scapy adlı bir Python kütüphanesini kullanmak ve kullanıcıdan girdi almak için gerekli olan optparse kütüphanesini içe aktarır.

#Kullanıcıdan IP Adresi Girişi Almak:

python

def get_user_input():
    parse_object = optparse.OptionParser()
    parse_object.add_option("-i","--ipaddress", dest="ip_address", help="Enter IP Address")

    (user_input, arguments) = parse_object.parse_args()

    if not user_input.ip_address:
        print("Enter IP Address")

    return user_input

#Bu fonksiyon, kullanıcıdan bir IP adresi girmesini ister. Kullanıcının girdiği IP adresi, programın devamında kullanılacaktır.

#Ağı Tara ve Sonuçları Göstermek:

python

def scan_my_network(ip):
    arp_request_packet = scapy.ARP(pdst=ip)
    broadcast_packet = scapy.Ether(dst="ff:ff:ff:ff:ff:ff")
    combined_packet = broadcast_packet / arp_request_packet
    (answered_list, unanswered_list) = scapy.srp(combined_packet, timeout=1)
    answered_list.summary()

#Bu fonksiyon, ağı tarar. İlk olarak, hedef IP adresine ARP (Address Resolution Protocol) isteği gönderir. Bu, belirli bir IP adresine sahip cihazın MAC adresini çözmek için kullanılır. Ardından, bu isteği yayınlar (broadcast). Son olarak, bu iki paketi birleştirir ve ağdaki cihazlardan gelen cevapları bekler. Cevapları ekrana yazdırır.

#Ana Program Akışı:


user_ip_address = get_user_input()
scan_my_network(user_ip_address.ip_address)

#Bu kısım, kullanıcının girdiği IP adresini alır ve scan_my_network fonksiyonunu bu IP adresi ile çağırarak ağı tarar.
