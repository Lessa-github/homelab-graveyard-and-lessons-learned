# Caso 04: Wazuh Cluster (6 GB) vs. Velociraptor (67 MB)

A sabedoria convencional diz para subir um cluster completo de Wazuh com indexador OpenSearch e dashboard Kibana.

No nosso hardware físico (onde 32 GB de RAM precisam alimentar mais de 15 serviços e laboratórios de IA), gastar 20% da memória total em JVMs não fazia sentido de engenharia.

Adotamos o **Velociraptor**:
* Binário Go único de 40 MB.
* 67 MB de RAM física consumida.
* Poder de busca forense superior via VQL em tempo real.
