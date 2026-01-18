1 what is a resource group ?

Logical container for related Azure resources (App Service, DB, monitoring, etc.)
Lifecycle unit (create / delete together) Billing & access scope
“J’ai utilisé un Resource Group pour isoler l’API et ses ressources associées.”

2 how is Azure App Service  a PaaS?
Managed platform to run web apps without managing servers
Azure provides:
OS (Linux)
Java runtime
Embedded Tomcat
HTTPS & certificates
Scaling & restart
📌 Sentence
“Azure App Service fournit un environnement PaaS avec runtime Java et HTTPS gérés.”

3  Reverse Proxy in azure ?
App Service always sits behind:
a reverse proxy
TLS termination
port mapping (80/443 → app)
📌 Sentence
“Le reverse proxy Azure gère TLS et le routage vers l’application.”

4 2️⃣ Deployment Model in Azure PAAS ?
🔹 ZIP / JAR deployment
You deployed via:
ZIP deploy
Single fat JAR
Key rule:
Azure does not guess how to start your app.
📌 Startup command (CRITICAL)
java -jar /home/site/wwwroot/app.jar


5 3️⃣ Runtime & Ports in Azure ?
🔹 Ports
Locally: Spring Boot → 8080
Azure App Service:
Azure injects PORT
App must listen on it
Azure maps it to 80/443
📌 Sentence
“Azure mappe automatiquement le port applicatif vers 80/443.”

6 how do you debug ? Logs & Debugging
🔹 Log Stream
Live logs
Shows startup errors
Shows JAR execution
You saw:
Old logs (container not restarted)
Parking page JAR
Wrong JAR path
Startup command not applied
📌 Sentence
“J’ai utilisé le Log Stream Azure pour diagnostiquer les erreurs de démarrage et valider l’exécution du JAR.”



