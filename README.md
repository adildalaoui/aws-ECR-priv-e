# 🚀 Créer et utiliser un registre privé AWS ECR (pas à pas)

Ce projet a pour objectif d’apprendre à utiliser **Amazon Elastic Container Registry (ECR)** pour stocker des images Docker dans un registre privé AWS.

J’ai utilisé cet exercice pour pousser deux images :
- `hello-world`
- `sonarqube`

---

# 🎯 Objectif

Comprendre comment :
- installer et configurer AWS CLI
- créer et utiliser un registre privé AWS ECR
- tagger une image Docker
- pousser une image vers AWS
- vérifier le stockage dans AWS

---

# 🧰 Prérequis

- Docker installé
- Un compte AWS
- Permissions IAM pour ECR
- Linux / WSL / MacOS

---

# ⚙️ Installation AWS CLI

Installation de AWS CLI v2 :

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
sudo apt install unzip
unzip awscliv2.zip
sudo ./aws/install
```

Vérifier l’installation :

```bash
aws --version
```

---

# 🔐 Configuration AWS

Configurer vos identifiants AWS :

```bash
aws configure
```

Entrer :
- AWS Access Key ID
- AWS Secret Access Key
- Region (ex: us-east-1)
- Output format (json)

---

# 📦 Création du repository ECR

Créer un repository privé dans AWS ECR :

```bash
aws ecr create-repository \
  --repository-name adildal \
  --region us-east-1
```

---

# 🔑 Connexion à ECR

Se connecter au registry AWS :

```bash
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 800393176284.dkr.ecr.us-east-1.amazonaws.com
```

---

# 🐳 Tag des images Docker

## Image Hello World

```bash
docker tag hello-world:latest 800393176284.dkr.ecr.us-east-1.amazonaws.com/adildal:v1
```

## Image SonarQube

```bash
docker tag sonarqube:latest 800393176284.dkr.ecr.us-east-1.amazonaws.com/adildal:v2
```

---

# 🚀 Push des images vers AWS ECR

## Hello World

```bash
docker push 800393176284.dkr.ecr.us-east-1.amazonaws.com/adildal:v1
```

## SonarQube

```bash
docker push 800393176284.dkr.ecr.us-east-1.amazonaws.com/adildal:sonar
```

---

# 📸 Preuves

Des captures d’écran des images envoyées sur AWS ECR sont disponibles dans ce repository.

---

# 🧠 Ce que j’ai appris

- Création d’un registry privé AWS ECR
- Authentification Docker avec AWS CLI
- Tagging d’images Docker
- Push d’images vers un registry cloud
- Gestion des images Docker dans AWS

---

# 💡 Résultat

Les images sont maintenant stockées dans un **registry privé AWS ECR** et peuvent être utilisées pour du déploiement cloud ou Kubernetes.

---

# 🔗 Commande clé résumée

```bash
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin <account-id>.dkr.ecr.us-east-1.amazonaws.com

docker tag IMAGE:TAG <account-id>.dkr.ecr.us-east-1.amazonaws.com/REPO:TAG

docker push <account-id>.dkr.ecr.us-east-1.amazonaws.com/REPO:TAG
```

---

# 🏁 Conclusion

Ce projet est une première étape vers le déploiement cloud avec Docker et AWS.


---
