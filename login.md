# Login Information

## AWS Cluster

The URL for the cluster is:

```
ec2-18-212-142-72.compute-1.amazonaws.com
```

#### Example

```
ssh -i [keyfile] [uname]@ec2-18-212-142-72.compute-1.amazonaws.com
```

where `[keyfile]` is the path to your private key paired with the key on the cluster and `[uname]` is your user name on the cluster. If my keyfile is `~/.ssh/id_ecdsa` and my user name is `newuser` it would look like this:

```
ssh -i ~/.ssh/id_ecdsa newuser@ec2-18-212-142-72.compute-1.amazonaws.com
```

## RStudio

The URL for RStudio is:

[http://ec2-54-156-54-210.compute-1.amazonaws.com/](http://ec2-54-156-54-210.compute-1.amazonaws.com/)

Navigate to this page using your web browser and enter your user name and provided password.

