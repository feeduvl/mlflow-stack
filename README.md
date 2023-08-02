# mlflow stack 

## Using mlflow

1. Install `mlflow` via `pip3 install mlflow`
2. Create a `.env`-file in your project with the following keys and values:

    ```sh
    MLFLOW_TRACKING_USERNAME=SERVICE_USERNAME
    MLFLOW_TRACKING_PASSWORD=SERVICE_PASSWORD
    MLFLOW_TRACKING_URI=https://mlflow-uvl.ifi.uni-heidelberg.de
    ```

3. Either:

   - use a tool like [https://direnv.net](https://direnv.net) to activate the `.env` file
   - load the environment variables manually
   - set the values directly via mlflow

4. Run your experiments
5. View them on [https://mlflow-uvl.ifi.uni-heidelberg.de](https://mlflow-uvl.ifi.uni-heidelberg.de)

## Operations

### Fresh deployment

1. Open Portainer
2. Switch to stacks
3. Delete current `mlflow`-stack
4. Create new stack -> from github
5. Enter repository url: `https://github.com/feeduvl/mlflow-stack`
6. Enter repository ref : `refs/heads/main`
7. Keep Compose path
8. Add environment variable `BASIC_AUTH`
   1. Create hashed credentials in your shell via `htpasswd -n SERVICE_USERNAME`
   2. Enter the service password
   3. Copy the returned value in the value field of `BASIC_AUTH`
9. Deploy the stack
10. Navigage to Containers -> mlflow and scroll to "Join a network"
11. Select `traefik-proxy` and `Join network`
12. Scroll up to actions and `Restart` the container.

### Maintenance deployment

1. Make the changes in this depository and test them locally via `docker-compose up -d`, `docker-compose logs -f` and a workload using the local mlflow configuration.
2. Back up the `/var/lib/docker/volumes/storage/_data` volume on the host
3. Make a fresh deployment
4. Copy back the backup
