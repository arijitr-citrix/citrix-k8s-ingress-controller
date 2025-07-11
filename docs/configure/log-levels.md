# Log levels

The logs generated by Netscaler ingress controller are available as part of [kubernetes logs](https://kubernetes.io/docs/concepts/cluster-administration/logging/). You can specify Netscaler ingress controller to log in the following log levels:

-  CRITICAL
-  ERROR
-  WARNING
-  INFO
-  DEBUG

By default, Netscaler ingress controller is set to log in `INFO` log level. If you want to specify Netscaler ingress controller to log in a particular log level then you need to specify the log level in the Netscaler ingress controller deployment YAML file before deploying the Netscaler ingress controller. You can specify the log level in the `spec` section of the YAML file as follows:

```YAML
apiVersion: v1
kind: Pod
metadata:
  name: citrixingresscontroller
  labels:
    app: citrixingresscontroller
spec:
      serviceAccountName: cpx
      containers:
      - name: citrixingresscontroller
        image: "quay.io/netscaler/netscaler-k8s-ingress-controller:3.1.34"
        env:
        # Set kube api-server URL
        - name: "kubernetes_url"
          value: "https://10.x.x.x:6443"
        # Set Netscaler Management IP
        - name: "NS_IP"
          value: "10.x.x.x"
        # Set log level
        - name: "LOGLEVEL"
          value: "DEBUG"
        - name: "EULA"
          value: "yes"
        args:
        - --feature-node-watch
          true
        imagePullPolicy: Always
```

## Modify the log levels

To modify the log level configured on the Netscaler ingress controller instance, you need to delete the instance and update the log level value in the following section and redeploy the Netscaler ingress controller instance:

```YAML
# Set log level
- name: "LOGLEVEL"
  value: "XXXX"
```

Once you update the log level, save the YAML file and deploy it using the following command:

    kubectl create -f citrix-k8s-ingress-controller.yaml