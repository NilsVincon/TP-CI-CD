#TP CI CD NILS VINCON 

Rapport 

-	What are testcontainers?
Testcontainers est une bibliothèque Java qui permet de créer des instances légères et isolées de services (comme des bases de données) dans des conteneurs Docker pour les tests d'intégration. Cela facilite la création d'un environnement de test proche de la production, tout en garantissant un état propre pour chaque test.
-	Document your Github Actions configurations.
on : Définit les événements qui déclenchent le workflow. Ici, il est configuré pour se déclencher lors de : - Un push sur les branches main ou develop. - Un pull request.
Jobs : Définit les jobs à exécuter. Dans ce cas, il y a un job nommé test-backend.
runs-on : Spécifie le système d'exploitation sur lequel le job s'exécute. Ici, vous utilisez Ubuntu 22.04.
Steps : Une liste d'étapes à exécuter dans le job :
Checkout : Récupère le code source de votre dépôt.
Set up JDK 17 : Installe Java JDK 17.
Build and test with Maven : Exécute Maven pour construire et tester votre application en utilisant le fichier pom.xml situé dans le dossier simple-api.

-	For what purpose do we need to push docker images?
Pousser des images Docker vers un registre facilite le partage, le déploiement et la gestion des versions des applications, garantissant une cohérence entre les différents environnements. Cela permet également d'automatiser le processus de livraison dans des pipelines CI/CD, rendant le déploiement plus rapide et fluide.

-	Document your quality gate configuration.
-	run: mvn -B verify org.sonarsource.scanner.maven:sonar-maven-plugin:sonar -Dsonar.projectKey=NilsVincon_TP-CI-CD -Dsonar.organization=nilsvincon -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=${{ secrets.SONAR_TOKEN }} --file ./simple-api/pom.xml

-B: Active le mode "batch", ce qui permet à Maven d'exécuter les tâches sans interactivité
Verify est une phase du cycle de vie Maven qui valide que le projet est correctement construit et que les tests sont passés.
org.sonarsource.scanner.maven:sonar-maven-plugin:sonar: Indique le plugin Sonar qui doit être exécuté pour réaliser l'analyse de code.
-Dsonar.projectKey=NilsVincon_TP-CI-CD: Définit la clé du projet dans SonarCloud, qui identifie de manière unique le projet analysé.
- Dsonar.organization=nilsvincon: Spécifie le nom de l'organisation sur SonarCloud à laquelle le projet appartient.
-Dsonar.host.url=https://sonarcloud.io: Indique l'URL de l'instance SonarCloud utilisée pour l'analyse.
-Dsonar.login=${{ secrets.SONAR_TOKEN }}: Utilise un token de connexion sécurisé (stocké dans les secrets GitHub) pour authentifier la requête auprès de SonarCloud.

--file ./simple-api/pom.xml: Spécifie le chemin du fichier pom.xml du projet Maven à analyser. Cela permet à Maven de savoir quel projet doit être traité.

