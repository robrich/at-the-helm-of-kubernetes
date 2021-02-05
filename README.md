At The Helm of Kubernetes: Repeatable Infrastructure Creation for Mere Mortals
==============================================================================

A live demo talk about Helm by [Rob Richardson](https://robrich.org/about).

See the slides at https://robrich.org/slides/at-the-helm-of-kubernetes/#/

## Run it

1. Install helm from https://github.com/helm/helm/releases and set `helm` in your path.

2. Build the docker image:

   ```
   cd src
   docker build -t atthehelm:v0.1.0 .
   cd ..
   ```

3. Run the template for the helm chart in the `chart` folder:

   ```
   helm template chart --set imageLabel=v0.1.0,ingressHost="",registry=""
   ```

   or start it directly in Kubernetes:

   ```
   helm template chart --set imageLabel=v0.1.0,ingressHost="",registry="" | kubectl apply -f -
   ```

4. Create a helm chart package:

   a. Install [helm-pack](https://github.com/thynquest/helm-pack) plugin:

      ```
      helm plugin install https://github.com/thynquest/helm-pack.git
      ```

   b. Package the chart in the `chart` folder:

      ```
      helm pack chart --app-version 0.1.0 --version 0.1.0 --destination dist --set imageLabel=v0.1.0,registry="",ingressHost=""
      ```

5. Run the packaged chart:

   ```
   helm install my-app ./dist/atthehelm-0.1.0.tgz --set ingressEnabled=false,replicas=2
   ```

   then see what you created:

   ```
   helm list
   ```

6. Remove the chart:

   ```
   helm uninstall my-app
   ```


## License

MIT, Copyright Richardson & Sons, LLC
