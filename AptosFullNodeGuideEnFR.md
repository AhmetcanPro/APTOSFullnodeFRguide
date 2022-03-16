# APTOSFullnodeFRguide
Guide français afin de mettre en place votre node pour Aptos. Guide originale (en anglais) : https://github.com/aykutarda/aykutarda/blob/main/APTOSFullNodeGuide.md
Traduit par : Huseyin#2669 / Translated in French by : Huseyin#2669

## AptosFullNode-Guide en Français
Comment installer un FullNode pour Aptos

## <a name='Contenu'></a>Contenu

* [1. Les Requis](#1-les requis)
* [2. L'installation étape par étape](#2-l'installation-étape-par-étape)

## 1. Les Requis

**Si vous lancez un Fullnode pour du développement ou pour effectuer des tests, il vous faudra au minimum :**

**CPU**: 2 cores
**Mémoire**: 4GB de RAM

*Si vous lancez un Fullnode à des fins de production, nous vous recommandons d'avoir au minimum**:

**CPU**: Intel Xeon Skylake ou un modèle plus récent, 4 cores
**Mémoire**: 8GB de RAM

## 2. L'installation étape par étape

**Première étape : Installez Screen et Docker**

```sudo apt install screen```

```screen -S homepage```

```sudo apt update```

```sudo apt install ca-certificates curl gnupg lsb-release wget -y```

```curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg```

```echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null```

```sudo apt update```

```sudo apt install docker-ce docker-ce-cli containerd.io -y```


**Deuxième étape: Installez Docker Compose**

```mkdir -p ~/.docker/cli-plugins/```

```curl -SL https://github.com/docker/compose/releases/download/v2.2.3/docker-compose-linux-x86_64 -o ~/.docker/cli-plugins/docker-compose```

```chmod +x ~/.docker/cli-plugins/docker-compose```

```sudo chown $USER /var/run/docker.sock```

**Troisième étape : Créer un fichier qu'on nommera Aptos et qui nous servira de dépositoire pour les fichiers de configs**

```mkdir $HOME/aptos```

```cd $HOME/aptos```

```wget https://raw.githubusercontent.com/aptos-labs/aptos-core/main/docker/compose/public_full_node/docker-compose.yaml```

```wget https://raw.githubusercontent.com/aptos-labs/aptos-core/main/docker/compose/public_full_node/public_full_node.yaml```

```wget https://devnet.aptoslabs.com/genesis.blob```

```wget https://devnet.aptoslabs.com/waypoint.txt```

**Quatrième étape : Lancement de notre node**

```docker compose up -d```

Félicitations, vous y êtes parvenu !

**Codes intéressant à noter quelque part :**

**Pour checker le statut sync**

```curl 127.0.0.1:9101/metrics 2> /dev/null | grep aptos_state_sync_version | grep type```

**Pour accéder au logs :**

```docker logs -f aptos-fullnode-1 --tail 5000```
