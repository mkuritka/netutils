# Network utils


### bash in network utils
```bash
kubectl run -it --rm netutils --restart=Never --image=kuritka/netutils -- bin/sh
```
to install whatewer you need run this:

```bash
apk add curl
```


### getting nslookup of service

```bash
kubectl run -it --rm netutils --restart=Never --image=netutils/kuritka -- nslookup rabbit-mq.onho-dev
```

where `rabbit-mq` is service name and `onho-dev` is namespace


### infinite sleep
```bash
kubectl run -it --rm netutils --restart=Never --image=kuritka/netutils -- /bin/sleep infinity
```

or

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: sleep
  namespace: mutant-test
  labels:
    app: sleep
spec:
  replicas: 1
  selector:
    matchLabels:
      app: sleep
  template:
    metadata:
      labels:
        app: sleep
    spec:
      containers:
        - name: sleep
          image: kuritka/netutils
          command: ["/bin/sleep","infinity"]
          imagePullPolicy: IfNotPresent
```
