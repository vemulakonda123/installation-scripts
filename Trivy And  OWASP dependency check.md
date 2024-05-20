Going to scan dependences which are using in our project (java====pom.xml,,,,,,nodejs====package.json,,,,,,,,,,python=====requirements.txt).
1) Trivy has access to NVD(national vulnerabuls database) which contains all vulnerability  from 2002 to 2024...
2) trivy download that database and compare that database with our dependences..
3) trivy is more better than OWASP dependency check because OWASP has only access to NVD,,but trivy can access to other databases like redhat linux,,other linux flavours 

scan vulnerability 




---INSTALLATION STEPS---

sudo apt-get install wget apt-transport-https gnupg lsb-release

wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | gpg --dearmor | sudo tee /usr/share/keyrings/trivy.gpg > /dev/null

echo "deb [signed-by=/usr/share/keyrings/trivy.gpg] https://aquasecurity.github.io/trivy-repo/deb $(lsb_release -sc) main" | sudo tee -a /etc/apt/sources.list.d/trivy.list

sudo apt-get update

sudo apt-get install trivy


---COMMANDS---

trivy image imagename

trivy fs --security-checks vuln,config   Folder_name_OR_Path

trivy image --severity HIGH,CRITICAL image_name

trivy image -f json -o results.json image_name

trivy repo repo-url

trivy k8s --report summary cluster

*******************************************************************************************************************************************************************





