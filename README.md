# Greenpeace Planet 4 Architecture

![Architecture](media/arch-diagram.png)

## Architecture Components

1. **UI** - A ReactJS Front End component
2. **Backend** - A NodeJS API for consuming data. Also handles consuming messages from Kafka and persisting them to the Database
3. **Database** - A Mongo Database for persisting event data.
4. **Kafka Topic** - Used for streaming event data from consuming apis to the backend/database.
5. **Common API** - Camel ingress interface for Event data.
6. **ControlShift Consumer** - Camel interface for consuming event data from the Control Shift Labs external service.
7. **Open Social Consumer** - Camel interface for consuming event data from the Open Social external service.

## Automated Deployment

This project can be deployed through GitOps. In order to do this, you first need a Kubernetes or OpenShift cluster with the following operators deployed.

* [Eunomia](https://github.com/kohlstechnology/eunomia.git)
* [Strimzi](https://strimzi.io/)

Deployment assumes you have the following namespaces created.

* `p4-dev` for development
* `p4-demo` for automated deployment

The automation DOES NOT create these namespaces and we do not assume the automation will have that permission.

Once the namespaces are created, you can deploy the whole lot by running:

```
kubectl apply -f manifests
```

This will kick off a GitOps workflow that will begin running automation in each of the component repos as kubernetes jobs. You can follow the action by watching the jobs. The jobs will run in `p4-dev` but will deploy to `p4-demo`.

```
kubectl get jobs -n p4-dev
```
