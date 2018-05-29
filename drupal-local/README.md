### Apply the all-in-one yaml to deploy the app
`kubectl apply -f drupal-all-in-one.yaml`

### Clone the repo containing the mysql script
`git clone https://github.com/ids/drupal-k8s.git`

### Copy the drupaldb_sample.sql to each mariadb pod
`kubectl get pods`
`kubectl cp drupal-k8s/data/drupaldb_sample.sql drupal-galera-*******:/var/lib/mysql/`

- Repeat this for each galera pod

### Create the drupaldb database on each mariadb pod
`kubectl exec -it drupal-galera-******`
`mysql -pFender2000`
`create database drupaldb;`
`exit`
`mysql -pFender2000 < /var/lib/mysql/drupaldb_sample.sql`

- Repeat this for each galera pod

### Test connectivity to the application
`kubectl get svc`

- Copy the IP Address for the **drupal-frontend-svc**
- Test in a web browser
- Update the bzt test yaml with the new IP and perform a loadtest
