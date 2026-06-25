# Infraestrutura do Rolê Fortal 🌊 
### Aplicativo idealizado para centralizar o que está ocorrendo em fortaleza.

---

### 📦 Como rodar
#### ☸️ Com Kubernetes
- Crie e rode um cluster local, usei o *Minikube*
- Suba os pods e jobs aplicando os seguintes arquivos .yaml dentro da pasta "k8s/"
```
1 - kubectl apply -f pv.yaml
2 - kubectl apply -f pvc.yaml
3 - kubectl apply -f backend-fetcher.yaml
4 - kubectl apply -f backend-web.yaml
5 - kubectl apply -f frontend.yaml
```
Rode o comando: *minikube service frontend* para visualizar o Frontend do projeto.

Verificar os pods rodando e outras informações: *kubectl get all*

#### 🐋 Com Docker
Rode os comandos na raiz do projeto:
```
1 - Docker compose build
2 - Docker compose up
```
- Frontend acesso no *localhost:3000*
- Backend acessa no *localhost:5001*

---

### 🐋 Estrutura de contêineres 
3 Contêineres:
- **Backend-Fetcher**: faz a busca por conteúdo em loop a cada 5min e guarda em JSON num arquivo para o backend-web expôr
- **Backend-Web**: consome o banco JSON e compartilha para outros contêineres via web 
- **Frontend**: consome os dados do backend via web e centraliza o conteúdo para o usuário

### ☸️ Configuração no kubernetes
1) **backend-fetcher.yaml**: organiza o POD do fetcher e usa o PVC para persistência de dados. OBS: Devo transformá-lo em CronJob depois.
2) **backend-web.yaml**: organiza o POD do web e consome os dados persistidos no PVC.
3) **pvc.yaml**: solicita um armazenamento para realizar os serviços do backend.
4) **pv.yaml**: cria o armazenamento compatível com pvc
5) **frontend.yaml**: POD do FrontEnd.

---

### 💻 Futuramente
- Fazer deploy num Desktop em Nuvem como Github Desktop
- Integrar com banco de dados em nuvem como firebase
- Adicionar mais fontes de notícias
- Ajustar interface

---

### 📰 Conteúdo centralizado
#### Atual:
- **O Povo**: É o **segundo maior** em circulação no estado e o mais antigo em funcionamento em Fortaleza, fundado em 1928.

#### Vai ser adicionado:
- **Diário do Nordeste**: É o jornal com a **maior tiragem** no Estado do Ceará, com forte cobertura em Fortaleza e região.
- **O Estado**: Tradicional veículo com presença online e impressa, cobrindo política, economia e geral.
- **G1 Ceará**: Portal de notícias vinculado à Rede Globo, com ampla cobertura estadual e capital.
- **GC+**: Portal do grupo R7, conhecido por suas seções de entretenimento, cultura e notícias policiais.
- **Ceará Agora**: Veículo que foca em notícias "bombásticas" e últimos acontecimentos do estado.
- **Tribuna do Ceará**: Um dos jornais mais tradicionais do estado, com atualizações diárias.
- **Portal Terra da Luz**: Focado especificamente em informar os principais acontecimentos da cidade de Fortaleza.
- **A Notícia do Ceará**: Site de últimas notícias completo e confiável para a região.
- **Jornal do Brasil** (ou portais de notícias locais como o **GCMAIS**): Frequentemente citados em listas de mídia local para cobertura de eventos e política.
