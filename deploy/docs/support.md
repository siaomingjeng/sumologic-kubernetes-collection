# Customer Issues Playbook

For all customer issues Open Source Collection team needs to receive information mentioned
in [Basic information](#basic-information) section.
[Additional information](#additional-information-specific-for-type-of-customer-issue) may be needed for specific types of customer issues.

- [Basic information](#basic-information)
- [Additional information specific for type of customer issue](#additional-information-specific-for-type-of-customer-issue)
  - [Wrong format of logs in Sumo](#wrong-format-of-logs-in-sumo)
  
## Basic information

- Version of Sumo Logic Kubernetes Collection Helm Chart, e.g.

  ```bash
  $ helm ls -A
  NAME            NAMESPACE       REVISION        UPDATED                                 STATUS          CHART           APP VERSION
  collection      sumologic       1               2022-02-18 11:51:19.646037586 +0000 UTC deployed        sumologic-2.5.1 2.5.1
  ```

- User applied values for Sumo Logic Kubernetes Collection Helm Chart, e.g.

  ```bash
  helm get values <RELEASE_NAME> -n <NAMESPACE>  > user_values.yaml
  ```

- All values for Sumo Logic Kubernetes Collection Helm Chart, e.g.

  ```bash
  helm get values <RELEASE_NAME> -n <NAMESPACE> -a > all_values.yaml
  ```

- If non helm installation is used then please provide all commands used to install Sumo Logic Kubernetes Collection along with all output files.

  - Example 1

    When commands below are used, please send these commands and `sumologic.yaml` file

    ```bash
    kubectl run tools \
    -i --quiet --rm \
    --restart=Never \
    --image sumologic/kubernetes-tools:2.9.0 -- \
    template \
    --name-template 'collection' \
    --set sumologic.accessId='<ACCESS_ID>' \
    --set sumologic.accessKey='<ACCESS_KEY>' \
    --set sumologic.clusterName='<CLUSTER_NAME>' \
    | tee sumologic.yaml

    kubectl apply -f sumologic.yaml
    ```

  - Example 2

    When commands below are used, please send these commands, `sumologic.yaml` and `values.yaml`

    ```bash
    helm template \
    collection --namespace sumologic \
    -f values.yaml \
    /sumologic/deploy/helm/sumologic > sumologic.yaml
    kubectl apply -f sumologic.yaml
    ```

- Kubernetes version, e.g.

  ```bash
  $ kubectl version
  Client Version: version.Info{Major:"1", Minor:"21+", GitVersion:"v1.21.9-3+5bfa682137fad9", GitCommit:"5bfa682137fad91088ec83cd6913bccb75401dc9", GitTreeState:"clean", BuildDate:"2022-01-26T21:59:57Z", GoVersion:"go1.16.13", Compiler:"gc", Platform:"linux/amd64"}
  Server Version: version.Info{Major:"1", Minor:"21+", GitVersion:"v1.21.9-3+5bfa682137fad9", GitCommit:"5bfa682137fad91088ec83cd6913bccb75401dc9", GitTreeState:"clean", BuildDate:"2022-01-26T21:55:03Z", GoVersion:"go1.16.13", Compiler:"gc", Platform:"linux/amd64"}
  ```

- Cloud provider, e.g. (`AWS`, `Azure`, `GCP`, `KOPS`)

- Customer `OrgID` and `Deployment` to access data in Sumo

## Additional information specific for type of customer issue

### Wrong format of logs in Sumo

- Container runtime (Docker, containerd, CRI-O)
- Example logs that are got using two methods:
  - using `kubectl logs <POD_NAME> -n <namespace>`
  - file with logs from Pod from `/var/log/containers/` directory on Kubernetes node
- Expected form of logs in Sumo
