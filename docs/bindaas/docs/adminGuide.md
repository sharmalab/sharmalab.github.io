It is possible to administer Bindaas without the AdminConsole UI. A UI however makes it very easy to manage a Bindaas instance and create APIs. In some production environment it may be required to deploy Bindaas services and stand-alone piece without the AdminConsole. This article describes the role of various configuration files and how they can be changed to configure Bindaas.

### Remove AdminConsole from standard distribution
Delete the `bindaas-web-console-0.0.1.jar` from the `$BINDAAS_HOME/bundles/`system directory and restart Bindaas

```bash
cd $BINDAAS_HOME/bundles/system
rm bindaas-web-console-0.0.1.jar
```

### Removing Security Dashboard
Delete the `security-dashboard-0.0.1.jar` from the `$BINDAAS_HOME/bundles/system` directory and restart Bindaas.

```bash
cd $BINDAAS_HOME/bundles/system
rm security-dashboard-0.0.1.jar
```

### Changing AdminConsole Default Port
Edit the `config.ini` located under `$BINDAAS_HOME/bin/configuration` directory and change the following property

```bash
org.osgi.service.http.port=8081
```

### Changing Middleware(service) Default Host/Port
Edit the `bindaas.config.json` file under `$BINDAAS_HOME/bin` directory and change following properties

```bash
"host": "0.0.0.0"
"port": 9099
```
If you are using the Query Browser from the AdminConsole to interact with the APIs you will also need to change the proxy URL as follows

```bash
"proxyUrl": "http://myProxy.org" # This must correspond to the host and port set above
```

### Enable/Disable Authentication
Edit the `bindaas.config.json` file under `$BINDAAS_HOME/bin` directory and change following properties

```bash
"enableAuthentication": true
```

### Enable/Disable Authorization
Edit the `bindaas.config.json` file under `$BINDAAS_HOME/bin` directory and change following properties
```bash
"enableAuthorization": true
```

Authorization is only enabled if Authentication flag is set to true

### Enable/Disable Audit
Edit the `bindaas.config.json` file under `$BINDAAS_HOME/bin` directory and change following properties
```bash
"enableAudit": true
```

### Changing Authorization Provider
Edit the `bindaas.config.json` file under `$BINDAAS_HOME/bin` directory and change following properties

```bash
"authorizationProviderClass": "edu.emory.cci.bindaas.security_dashboard.service.AuthorizationProviderImpl"
```

### Changing Default Admin Password for AdminConsole
Edit the `bindaas.authentication.properties` file under `$BINDAAS_HOME/bin` directory and add as many user/passwd as you like

```bash
admin=password,
temp1=temp1,
UserA=PassA
```

### Configuring Mail
The Mail service is used internally by Bindaas to send notifications (if enabled) about new user enrollment. Hence, it is only relevant if AdminConsole is installed. The `mailService.properties` file under `$BINDAAS_HOME/bin` directory can be edited to change default Mail settings

```bash
mail.smtp.starttls.enable=true
mail.smtp.port=587
password=passwd
mail.smtp.auth=true
mail.smtp.host=smtp.gmail.com
username=user@gmail.com
```