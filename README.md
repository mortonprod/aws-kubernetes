# Costs

## Micro

* t3.micro	$0.006 per Hour	$0.008 per Hour
** Total per month = 5.76

## Small
* t3.small	$0.013 per Hour	$0.017 per Hour
** Total per month = 12.24

## xLarge

* t3.xlarge	$0.104 per Hour	$0.132 per Hour
** Total per month = 95.04

## EBS

* SSD (gp2) 0.1/GB x 100 GB
* Total per month = 1

# Setup Requirements

* Will need to be able to start and stop the system.
** Remove all master and worker nodes
** Need to be able to deploy all pods we had in pipeline
* Need to be able to store data and reattach
** This mean attaching old EBS volumes with data we plan to keep
** Also means ditching EBS volumes we stored old cluster state in
** Back up lots of data to s3


# Initial

```bash
kops create cluster  \
    --zones=eu-west-1a,eu-west-1b,eu-west-1c \
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