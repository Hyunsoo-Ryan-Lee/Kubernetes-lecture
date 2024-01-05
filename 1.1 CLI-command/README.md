1. nginx pod 실행
> kubectl run nginx-pod nginx --image=nginx

1. Start a single instance of nginx.
> kubectl run nginx --image=nginx

1. Start a single instance of hazelcast and let the container expose port 5701 .
> kubectl run hazelcast --image=hazelcast --port=5701

1. Start a single instance of hazelcast and set environment variables "DNS_DOMAIN=cluster" and "POD_NAMESPACE=default" in the container.
> kubectl run hazelcast --image=hazelcast --env="DNS_DOMAIN=cluster" --env="POD_NAMESPACE=default"

1. Start a replicated instance of nginx.
> kubectl run nginx --image=nginx --replicas=5

1. Dry run. Print the corresponding API objects without creating them.
> kubectl run nginx --image=nginx --dry-run

1. Start a single instance of nginx, but overload the spec of the deployment with a partial set of values parsed from JSON.
> kubectl run nginx --image=nginx --overrides='{ "apiVersion": "v1", "spec": { ... } }'

1. Start a single instance of busybox and keep it in the foreground, don't restart it if it exits.
> kubectl run -i --tty busybox --image=busybox --restart=Never

1. Start the nginx container using the default command, but use custom arguments (arg1 .. argN) for that command.
> kubectl run nginx --image=nginx -- <arg1> <arg2> ... <argN>

1. Start the nginx container using a different command and custom arguments.
> kubectl run nginx --image=nginx --command -- <cmd> <arg1> ... <argN>

1. Start the perl container to compute π to 2000 places and print it out.
> kubectl run pi --image=perl --restart=OnFailure -- perl -Mbignum=bpi -wle 'print bpi(2000)'

1. port forward
>kubectl port-forward nginx-pod 8080:80