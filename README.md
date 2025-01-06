# Laboratorium 9: Programowanie FullStack w Chmurze Obliczeniowej 

## Utworzenie przestrzeni nazw
Utworzono dwie przestrzenie nazw kolejno appns-a oraz appns-b za pomocą plików manifestów appns_a.yaml oraz appns_b.yaml. 

![image](https://github.com/user-attachments/assets/c195603c-36c8-48d0-acbe-841071416118)

## Utworzenie obiektów Deployment
Utworzono dwa obiekty typu deployment każdy w innej przestrzeni nazw (app-a w appns-a i analogicznie app-b). Każdy deployment posiada po dwie repliki. Dla każdego obiektu Deployment utworzono obiekt Service typu NodePort.

![image](https://github.com/user-attachments/assets/0e0a4798-26d9-463e-be83-919ce2aa547c)

![image](https://github.com/user-attachments/assets/fe7ca51d-2eb2-4c2d-88b7-583375cdf72a)

## Utworzenie obiektów Network Policy
Zabroniono wszelkiej komunikacji pomiędzy obiektami uruchomionymi w przestrzeni nazw appns-a oraz appns-b via dokumentacja Kubernetesa. Ponieważ polityki działają na zasadzie zezwoleniea ruchu, aby zabronić komunikacji zastosowano restrykcyjną politykę, która ogranicza całkowicie ruch. Dodatkowo uwtorzono dwie kolejne poliyki, które stanowia wyjatek i zezwalają na ruch do przestrzeni nazw ingress-nginx, w której działa kontroller Ingress. Na poniższym zrzucie jest widoczne ze pody nie mogą się ze sobą komunikować.

![image](https://github.com/user-attachments/assets/036440ab-4cfd-47c3-8582-213f57abe691)

## Utworzenie kontrolera Ingress Nginx i obiektów Ingress
Ponieważ obiekty Deployment są w różnych przestrzeniach nazw utworzono w każdej obiekt Ingress, tak by możliwe było znalezienie endpointów. Aplikacja app-a jest dostępna pod adresem a.lab9.net
natomiast app-b jest dostępna pod adresem b.lab9.net. Dodatkowo utworzono również domyślny backend.

![image](https://github.com/user-attachments/assets/4db68b06-bd65-49d7-b636-7adceb58a81f)

![image](https://github.com/user-attachments/assets/d97d56de-8515-4db9-8247-1f816af530c1)

Dostęp do domyślnego backendu działa poprawnie.

![image](https://github.com/user-attachments/assets/2a93da27-2032-4434-ac5d-f96bb13b1980)

Jednak napotkałam problem z dostępem do app-a oraz app-b z poziomu Ingress.

![image](https://github.com/user-attachments/assets/b2eb5f66-21c3-404c-8ec4-0240ee8ebd86)

Logi z kontrolera Ingress Nginx.

![image](https://github.com/user-attachments/assets/3fb1c769-78a2-451d-a486-1a1096a3b5ca)

Network Policy posiadają charakter addytywny, stąd tez powienien zadziałać wyjatek w postaci zezwolenia na ruch z i do przestrzeni nazw ingress-nginx dla appns-a i appns-b. 

![image](https://github.com/user-attachments/assets/1c28127e-bcbd-4e6a-8337-60cf12a377a3)

![image](https://github.com/user-attachments/assets/3890e7b3-e84b-489a-98d7-90811f20c413)

Po usunięciu network policy dostęp do app-a oraz app-b działa poprawnie.

![image](https://github.com/user-attachments/assets/762664d0-89a2-49bd-86cd-229e96ced6e7)

![image](https://github.com/user-attachments/assets/7c665322-b6b1-4f38-8483-72b3fd977c37)

Aby ominąć ten probelm testowałam rózne konfiguracje polityk sieciowych, jednak nie udało mi się rozwiązać probelmu. Planuję w dalszym ciągu analizować problem i znaleźć rozwiązanie.

<hr>







