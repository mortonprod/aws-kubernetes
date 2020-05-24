# Costs

Spot instances

## Micro

* t3.micro	$0.0035 per Hour
  * Total per month = 2.52

## Small
* t3.small	$0.0071 per Hour
  * Total per month = 5.112

## xLarge

* t3.xlarge	$0.0566 per Hour
  * Total per month = 40.32

## EBS

* SSD (gp2) 0.1/GB x 100 GB
* Total per month = 1

# Setup Requirements

* Will need to be able to start and stop the system.
  * Remove all master and worker nodes
  * Need to be able to deploy all pods we had in pipeline
* Need to be able to store data and reattach
  * This mean attaching old EBS volumes with data we plan to keep
  * Also means ditching EBS volumes we stored old cluster state in
  * Back up lots of data to s3


# Initial

```bash
kops create cluster  \
    --zones=eu-west-2a,eu-west-2b,eu-west-2c \
    --cloud=aws \
    --kubernetes-version v1.15.0 \
    --master-count=3 \
    --master-size t3.small \
    --name=kubernetes.alexandermorton.co.uk \
    --networking=calico \
    --node-count=1 \
    --node-size t3.xlarge \
    --state=s3://state.kubernetes.alexandermorton.co.uk \
    --dry-run --output yaml | tee kubernetes.alexandermorton.co.uk.yaml
```