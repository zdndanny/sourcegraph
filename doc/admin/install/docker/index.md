# Install Sourcegraph with Docker

## Prerequisites

[Docker](https://docs.docker.com/engine/installation/) is required.

## Step 1: Run Sourcegraph

```
docker run \
  --publish 7080:7080 --publish 2633:2633 --rm \
  --volume ~/.sourcegraph/config:/etc/sourcegraph \
  --volume ~/.sourcegraph/data:/var/opt/sourcegraph \
  --volume /var/run/docker.sock:/var/run/docker.sock \
  sourcegraph/server:2.13.5
```

When Sourcegraph is ready, continue at http://localhost:7080.

## Step 2: Add repositories

After creating an account, go to the **Configuration** page in the site admin area.

Click **Add GitHub.com repositories** to add all repositories associated with your GitHub.com account, or see [how to add repositories from other code hosts](../../repo/add.md).

## Step 3: Start searching your code

**Done!** You're ready to search your code.

## Next steps

- [Configure your Sourcegraph instance](../../site_config/index.md)
- [Configure code intelligence](../../../extensions/language_servers/index.md)
- [Deploy Sourcegraph on AWS](../../install/docker/aws.md)
- [Deploy Sourcegraph on Google Cloud Platform](../../install/docker/google_cloud.md)
- [Deploy Sourcegraph on Digital Ocean](../../install/docker/digitalocean.md)

## File system performance on Docker for Mac

There is a [known issue](https://github.com/docker/for-mac/issues/77) in Docker for Mac that causes slower than expected file system performance on volume mounts, which impacts the performace of search and cloning.

To achieve better performance, you can do any of the following:

- For better clone performance, clone the repository on your host machine and then [add it to Sourcegraph Server](../../repo/add.md#add-repositories-already-cloned-to-disk).
- Try adding the `:delegated` suffix the data volume mount. [Learn more](https://github.com/docker/for-mac/issues/1592).
  ```
  --volume ~/.sourcegraph/data:/var/opt/sourcegraph:delegated
  ```
- Run Sourcegraph Server on Linux, or use the [Kubernetes cluster deployment option](https://github.com/sourcegraph/deploy-sourcegraph) for even larger scale.
