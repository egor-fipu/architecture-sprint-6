```commandline
kubectl get pods
NAME                            READY   STATUS    RESTARTS      AGE
scaletestapp-84fbd7cb88-75kkt   1/1     Running   2 (32s ago)   28m
scaletestapp-84fbd7cb88-gq4zm   1/1     Running   0             66s
```

```commandline
kubectl get hpa
NAME               REFERENCE                 TARGETS           MINPODS   MAXPODS   REPLICAS   AGE
scaletestapp-hpa   Deployment/scaletestapp   memory: 30%/80%   1         10        2          28m
```

```commandline
kubectl describe hpa scaletestapp-hpa
Name:                                                     scaletestapp-hpa
Namespace:                                                default
Labels:                                                   <none>
Annotations:                                              <none>
CreationTimestamp:                                        Sat, 28 Dec 2024 09:17:17 +0700
Reference:                                                Deployment/scaletestapp
Metrics:                                                  ( current / target )
  resource memory on pods  (as a percentage of request):  30% (6334464) / 80%
Min replicas:                                             1
Max replicas:                                             10
Deployment pods:                                          2 current / 2 desired
Conditions:
  Type            Status  Reason               Message
  ----            ------  ------               -------
  AbleToScale     True    ScaleDownStabilized  recent recommendations were higher than current one, applying the highest recent recommendation
  ScalingActive   True    ValidMetricFound     the HPA was able to successfully calculate a replica count from memory resource utilization (percentage of request)
  ScalingLimited  False   DesiredWithinRange   the desired count is within the acceptable range
Events:
  Type    Reason             Age   From                       Message
  ----    ------             ----  ----                       -------
  Normal  SuccessfulRescale  86s   horizontal-pod-autoscaler  New size: 2; reason: memory resource utilization (percentage of request) above target
```