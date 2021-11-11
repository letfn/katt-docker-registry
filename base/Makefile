build: clean ../main.yaml

../main.yaml: main.yaml
	kustomize build >$@

main.yaml: clean/main.yaml
	kustomize build clean >$@

clean/main.yaml: clean/values.yaml
	-helm repo add twuni https://helm.twun.io
	helm repo update
	helm template docker-registry twuni/docker-registry \
		--version 1.14.0 --namespace=docker-registry --values=clean/values.yaml --include-crds --kube-version 1.21 >$@

.PHONY: clean
clean:
	rm -f ../main.yaml main.yaml clean/main.yaml
