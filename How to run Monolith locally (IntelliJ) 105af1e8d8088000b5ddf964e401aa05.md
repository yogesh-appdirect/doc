# How to run Monolith locally (IntelliJ)

# 📕 Part 1: **Prerequisites**

- VPN connection
- Complete the [Dev Machine Setup](https://knowledge.appdirect.tools/services/monolith/local-setup/Dev_Machine_setup) → set of softwares required
- Use JDK 8 ([download Amazon Corretto 1.8.0_412](https://github.com/corretto/corretto-8/releases)) → use mentioned jdk version to avoid any trouble
- To avoid OutOfMemoryError when running large JAVA programs (like AppDirect), set the MAVEN_OPTS environment variable by editing your .mavenrc (create one at ~/.mavenrc if it doesn't exist) and adding the lines

```jsx
export MAVEN_DEBUG_OPTS="-Xdebug -Xnoagent -Djava.compiler=NONE -Xrunjdwp:transport=dt_socket,server=y,suspend=n,address=8000"
export MAVEN_OPTS="-Xms1024m -Xmx4096m -noverify -XX:MaxMetaspaceSize=760m"
```

---

# 💡 Part 2: Docker Images

Pull Required Images

```yaml
docker pull docker.appdirect.tools/appdirect/appdirectdb:latest
docker pull docker.appdirect.tools/appdirect/memcached:latest
docker pull docker.appdirect.tools/appdirect/rabbitmq:latest
docker pull docker.appdirect.tools/appdirect/jbilling:latest
docker pull docker.appdirect.tools/appdirect/jbillingdb:latest
docker pull docker.appdirect.tools/appdirect/ad-theme-compiler:latest
```

Run Required Images

```yaml
docker run --name appdirectdb -d -p 3306:3306 docker.appdirect.tools/appdirect/appdirectdb:latest
docker run --name memcached -d -p 11211:11211 docker.appdirect.tools/appdirect/memcached:latest
docker run --name rabbitmq -d -p 5672:5672 -p 15672:15672 docker.appdirect.tools/appdirect/rabbitmq:latest
docker run --name db -d -p 3307:3306 docker.appdirect.tools/appdirect/jbillingdb
docker run --name jbilling -d -p 8088:8080 --link db docker.appdirect.tools/appdirect/jbilling
docker run --name theme-compiler -d -p 5555:5555 docker.appdirect.tools/appdirect/ad-theme-compiler:latest
```

Confirm all dependencies are up and running using docker command, output should look like

![image.png](How%20to%20run%20Monolith%20locally%20(IntelliJ)%20105af1e8d8088000b5ddf964e401aa05/image.png)

---

# 🥇 Part 3: Implementation

*What steps do we need to take to implement the product?*

## 🔧 Technical Design Document

*What are the architecture and design decisions for the project?*

## 🔬 QA & Test Plan

*How will we ensure that the project meets quality standards and functions as intended?*

---

# 🚀 Part 4: Launch

## 🚛 Roll Out Plan

*For example:*

1. *Speaker notes clean up*
    - [ ]  *Polish up QA items*
    - [ ]  *Add metrics to file*
2. *Roll out for internal launch*
    - [ ]  *Release to Desktop with latest updates*
    - [ ]  *Flip feature flag*
3. *Beta Launch to Windows users*
    - [ ]  *Handoff document to support*

## 🛒 Pricing & Packaging

*Will the product be part of our free plan or only paid plans? Is it an add on?*

## 💌 Communications Plan

*When will communications happen? Who will be notified of this new feature? Will we send emails, in-app notifications?*

## 📡 GTM Brief

*What does sales/success need to know to be able to sell this feature? [Ideally, this is done well ahead of launch so they can start generating excitement.] Will they need to send comms to our sales-led customers?*

## 📊 Monitoring

*What dashboards will we need for monitoring (Amplitude, Mode, etc)? Who will be responsible? At what frequency will monitoring occur?*

---

# 🎁 Part 5: Impact

*For example:*

- *25% increase in user engagement within the first month.*
- *10% reduction in customer churn rate.*
- *Increase in average revenue per user by 15%.*

---

# 🗒️ Part 6: Notes

*For example:*

- *Consider a follow-up survey for more detailed user feedback.*
- *Collaborate with the marketing team for promotional content for the new feature.*
- *Monitor competitor responses and market changes.*
- Gettting error while running monolith, says `payment_duplicates_cim_8202` already exists
    
    Check in the Tomcat [Localhost](http://Localhost) Log window, if the error is same as the picture below, just delete the CREATE TABLE SQL query related to this table.
    
    ![Image shows the error related to  `payment_duplicates_cim_8202`](How%20to%20run%20Monolith%20locally%20(IntelliJ)%20105af1e8d8088000b5ddf964e401aa05/payment_duplicates_cim_8202.png)
    
    Error related to `payment_duplicates_cim_8202`
