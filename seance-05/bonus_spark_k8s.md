# Bonus : Déploiement de Spark sur Kubernetes (Kind)

## Présentation de la démarche

Dans le cadre de ce bonus optionnel de niveau Master, nous avons migré notre logique de traitement distribué d'un environnement **Spark Standalone** (Docker Compose) vers une infrastructure de production orchestrée par **Kubernetes (Kind)**.

Face à l'obsolescence et au déplacement des URLs des dépôts officiels du **Spark Operator** sur GitHub, nous avons fait preuve d'autonomie en concevant des manifestes YAML locaux complets afin de contourner les erreurs **404 Not Found** et de respecter les restrictions de sécurité imposées par l'API Kubernetes (`api-approved.kubernetes.io`).

---

# Étapes techniques de réalisation

## 1. Préparation du cluster Kind et du namespace

Le cluster Kubernetes local nommé **anfa** (déployé lors de la séance 3) a été réactivé.

Un namespace dédié a été créé afin d'isoler les composants Spark du reste du cluster.

```powershell
kubectl create namespace spark
```

---

## 2. Déploiement local du Spark Operator

Pour contourner l'absence du gestionnaire **Helm** sur le poste Windows, un fichier `spark-operator.yaml` a été créé.

Celui-ci définit :

* un **ServiceAccount** nommé `spark-operator` ;
* un **ClusterRole** accordant les permissions nécessaires ;
* un **ClusterRoleBinding** reliant le rôle au ServiceAccount ;
* un **Deployment** utilisant l'image officielle :

### Déploiement :

```powershell
kubectl apply -f spark-operator.yaml
```

---

## 3. Déclaration de la Custom Resource Definition (CRD)

Afin que Kubernetes reconnaisse l'objet `SparkApplication`, le fichier `spark-crd.yaml` a été créé puis appliqué.

L'annotation réglementaire suivante a été ajoutée pour satisfaire les contrôles de validation de Kubernetes.

```yaml
metadata:
  name: sparkapplications.sparkoperator.k8s.io

  annotations:
    api-approved.kubernetes.io: "https://github.com/kubeflow/spark-operator"
```

Application de la CRD :

```powershell
kubectl apply -f spark-crd.yaml
```

Résultat obtenu :

```text
customresourcedefinition.apiextensions.k8s.io/sparkapplications.sparkoperator.k8s.io created
```

---

## 4. Déploiement du Job Spark distribué

L'application Spark a ensuite été soumise grâce au manifeste `spark-job.yaml`.

Cette configuration permet de créer automatiquement :

* **1 Pod Driver (Master)**
* **2 Pods Executors (Workers)**

Commande :

```powershell
kubectl apply -f spark-job.yaml
```

Résultat :

```text
sparkapplication.sparkoperator.k8s.io/anfa-analyse-cluster-k8s created
```

---

# Validation et suivi de l'orchestration

Le suivi en temps réel a été effectué avec la commande :

```powershell
kubectl get pods -n spark -w
```

Les étapes suivantes ont pu être observées :

* détection de la ressource **SparkApplication** par le Spark Operator ;
* création et démarrage automatique du Pod **Driver** (`anfa-analyse-cluster-k8s-driver`) ;
* création dynamique des Pods **Executors** (`exec-1` et `exec-2`) ;
* exécution distribuée des traitements PySpark ;
* terminaison normale de tous les Pods avec le statut **Completed**.

---

# Conclusion et apports du mode Kubernetes

Cette implémentation démontre la grande portabilité de **PySpark**.

Le même code applicatif peut être exécuté sans modification sur :

* un poste local ;
* un cluster Spark Standalone ;
* un cluster Kubernetes orchestré.

L'utilisation de Kubernetes apporte plusieurs avantages :

* **scalabilité horizontale** grâce à l'ajout automatique d'instances ;
* **résilience** avec le redémarrage automatique des composants en cas de panne ;
* **élasticité** permettant d'adapter les ressources selon la charge ;
* **orchestration cloud-native** facilitant les déploiements, la maintenance et l'exploitation en production.

Cette approche rapproche ainsi l'architecture d'un environnement de production moderne utilisé dans les plateformes Big Data et les infrastructures Cloud.
