---
title: "Ahoy Build - ERROR [cli internal] load metadata for docker.io/govcms"
date: "2024-09-10"
categories: ["GovCMS", "Issue"]
---



## Original Error

I was encountering this issue as I run `ahoy build`:
```
> ahoy build
[+] Building 12.5s (2/2) FINISHED                                                                      docker:desktop-linux
 => [cli internal] load build definition from Dockerfile.cli                                                           0.0s
 => => transferring dockerfile: 1.43kB                                                                                 0.0s
 => ERROR [cli internal] load metadata for docker.io/govcms/govcms:10.x-latest                                        12.4s
------
 > [cli internal] load metadata for docker.io/govcms/govcms:10.x-latest:
------
failed to solve: govcms/govcms:10.x-latest: failed to resolve source metadata for docker.io/govcms/govcms:10.x-latest: failed to do request: Head "https://registry-1.docker.io/v2/govcms/govcms/manifests/10.x-latest": net/http: TLS handshake timeout
```
OR
```
> ahoy build
[+] Building 87.3s (35/35) FINISHED                                                                    docker:desktop-linux
 => [cli internal] load build definition from Dockerfile.cli                                                           0.0s
 => => transferring dockerfile: 1.43kB                                                                                 0.0s
 => [cli internal] load metadata for docker.io/govcms/govcms:10.x-latest                                               0.8s
 => [cli internal] load .dockerignore                                                                                  0.0s
 => => transferring context: 275B                                                                                      0.0s
 => [cli  1/12] FROM docker.io/govcms/govcms:10.x-latest@sha256:5f996887445a17ddb0cbf6148027bd4423fe06a616d8834ed1fc1  0.0s
 => [cli internal] load build context                                                                                  1.7s
 => => transferring context: 3.38MB                                                                                    1.6s
 => CACHED [cli  2/12] RUN mv /app/web/sites/all/modules /scaffold_modules   && rm -rf /app                            0.0s
 => CACHED [cli  3/12] RUN composer config --global github-oauth.github.com XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX   0.0s
 => CACHED [cli  4/12] COPY composer.* /app/                                                                           0.0s
 => CACHED [cli  5/12] COPY scripts /app/scripts                                                                       0.0s
 => CACHED [cli  6/12] COPY custom /app/custom                                                                         0.0s
 => CACHED [cli  7/12] RUN composer install --no-dev --no-interaction --no-suggest   && mkdir -p /app/web/sites/all    0.0s
 => CACHED [cli  8/12] COPY . /app                                                                                     0.0s
 => CACHED [cli  9/12] COPY .docker/config/cli/govcms.site.yml /app/drush/sites/                                       0.0s
 => CACHED [cli 10/12] RUN rm -Rf /home/.composer/vendor/bin                                                           0.0s
 => CACHED [cli 11/12] COPY .docker/scripts/sanitize.sh /tmp/sanitize.sh                                               0.0s
 => CACHED [cli 12/12] RUN chmod +x /tmp/sanitize.sh   && /tmp/sanitize.sh   && rm /tmp/sanitize.sh                    0.0s
 => [cli] exporting to image                                                                                           0.0s
 => => exporting layers                                                                                                0.0s
 => => writing image sha256:ce4ac8d7c524d94cab6b5b9df5ba69bfd74cd2a6094512d9e1ee4294ccffd2d2                           0.0s
 => => naming to docker.io/library/pwss-paas                                                                           0.0s
 => [cli] resolving provenance for metadata file                                                                       0.0s
 => [nginx internal] load build definition from Dockerfile.nginx-drupal                                                0.0s
 => => transferring dockerfile: 384B                                                                                   0.0s
 => WARN: FromAsCasing: 'as' and 'FROM' keywords' casing do not match (line 8)                                         0.0s
 => WARN: InvalidDefaultArgInFrom: Default value for ARG ${CLI_IMAGE} results in empty or invalid base image name (li  0.0s
 => [test internal] load build definition from Dockerfile.test                                                         0.0s
 => => transferring dockerfile: 323B                                                                                   0.0s
 => WARN: FromAsCasing: 'as' and 'FROM' keywords' casing do not match (line 8)                                         0.0s
 => WARN: InvalidDefaultArgInFrom: Default value for ARG ${CLI_IMAGE} results in empty or invalid base image name (li  0.0s
 => [php internal] load build definition from Dockerfile.php                                                           0.0s
 => => transferring dockerfile: 281B                                                                                   0.0s
 => WARN: FromAsCasing: 'as' and 'FROM' keywords' casing do not match (line 8)                                         0.0s
 => WARN: InvalidDefaultArgInFrom: Default value for ARG ${CLI_IMAGE} results in empty or invalid base image name (li  0.0s
 => [nginx internal] load metadata for docker.io/govcms/nginx-drupal:10.x-latest                                       0.8s
 => [php internal] load metadata for docker.io/library/pwss-paas:latest                                                0.0s
 => ERROR [test internal] load metadata for docker.io/govcms/test:10.x-latest                                         84.7s
 => ERROR [php internal] load metadata for docker.io/govcms/php:10.x-latest                                           84.6s
 => [nginx internal] load .dockerignore                                                                                0.0s
 => => transferring context: 275B                                                                                      0.0s
 => [nginx cli 1/1] FROM docker.io/library/pwss-paas:latest                                                            0.1s
 => [nginx internal] load build context                                                                                0.7s
 => => transferring context: 84B                                                                                       0.7s
 => CACHED [nginx stage-1 1/3] FROM docker.io/govcms/nginx-drupal:10.x-latest@sha256:ec9101ed074cec71e8ef4fc26b8486c5  0.0s
 => [nginx stage-1 2/3] COPY --from=cli /app/web /app/web                                                              3.8s
 => [nginx stage-1 3/3] COPY redirects-map.conf /etc/nginx/govcms-redirects-map.conf                                   0.0s
 => [nginx] exporting to image                                                                                         1.5s
 => => exporting layers                                                                                                1.5s
 => => writing image sha256:e295f9244b12fdb4bd56b7fd4d90c999da108281bdddfd050fb49008a5d97c81                           0.0s
 => => naming to docker.io/library/govcms-pwss-paas-nginx                                                              0.0s
 => [nginx] resolving provenance for metadata file                                                                     0.0s
 => [test auth] govcms/test:pull token for registry-1.docker.io                                                        0.0s
 => [php auth] govcms/php:pull token for registry-1.docker.io                                                          0.0s
------
 > [test internal] load metadata for docker.io/govcms/test:10.x-latest:
------
------
 > [php internal] load metadata for docker.io/govcms/php:10.x-latest:
------
failed to solve: govcms/php:10.x-latest: failed to resolve source metadata for docker.io/govcms/php:10.x-latest: failed to authorize: failed to fetch oauth token: Post "https://auth.docker.io/token": net/http: TLS handshake timeout

```





## Resolution Approach

I was able to solve it via editing Docker Engine/Daemon Configuration file:

![2024-09-10T143139](2024-09-10T143139.jpg)

And change the configuration to

```
{
  "builder": {
    "gc": {
      "defaultKeepStorage": "20GB",
      "enabled": true
    }
  },
  "experimental": false,
  "max-concurrent-downloads": 1,
  "max-concurrent-uploads": 1
}
```

Opening a new terminal and run the following

```
> docker login https://gitlab-registry-production.govcms.amazee.io/
Authenticating with existing credentials...
Login Succeeded
> sudo ahoy build
[+] Building 8.4s (49/49) FINISHED                                                                   docker:desktop-linux
 => [cli internal] load build definition from Dockerfile.cli                                                         0.0s
 => => transferring dockerfile: 1.43kB                                                                               0.0s
 => [cli internal] load metadata for docker.io/govcms/govcms:10.x-latest                                             1.5s
 => [cli auth] govcms/govcms:pull token for registry-1.docker.io                                                     0.0s
 => [cli internal] load .dockerignore                                                                                0.0s
 => => transferring context: 275B                                                                                    0.0s
 => [cli  1/12] FROM docker.io/govcms/govcms:10.x-latest@sha256:5f996887445a17ddb0cbf6148027bd4423fe06a616d8834ed1f  0.0s
 => [cli internal] load build context                                                                                4.7s
 => => transferring context: 249.70MB                                                                                4.6s
 => CACHED [cli  2/12] RUN mv /app/web/sites/all/modules /scaffold_modules   && rm -rf /app                          0.0s
 => CACHED [cli  3/12] RUN composer config --global github-oauth.github.com ghp_fhdV4ZH6ZvpRfiSJ4G2GCck0ULMAiD0Fn14  0.0s
 => CACHED [cli  4/12] COPY composer.* /app/                                                                         0.0s
 => CACHED [cli  5/12] COPY scripts /app/scripts                                                                     0.0s
 => CACHED [cli  6/12] COPY custom /app/custom                                                                       0.0s
 => CACHED [cli  7/12] RUN composer install --no-dev --no-interaction --no-suggest   && mkdir -p /app/web/sites/all  0.0s
 => CACHED [cli  8/12] COPY . /app                                                                                   0.0s
 => CACHED [cli  9/12] COPY .docker/config/cli/govcms.site.yml /app/drush/sites/                                     0.0s
 => CACHED [cli 10/12] RUN rm -Rf /home/.composer/vendor/bin                                                         0.0s
 => CACHED [cli 11/12] COPY .docker/scripts/sanitize.sh /tmp/sanitize.sh                                             0.0s
 => CACHED [cli 12/12] RUN chmod +x /tmp/sanitize.sh   && /tmp/sanitize.sh   && rm /tmp/sanitize.sh                  0.0s
 => [cli] exporting to image                                                                                         0.0s
 => => exporting layers                                                                                              0.0s
 => => writing image sha256:b03dc6f282d1484a8d326bda922438ccbe4ecfd1a3898796f87714192e85bce0                         0.0s
 => => naming to docker.io/library/pwss-paas                                                                         0.0s
 => [cli] resolving provenance for metadata file                                                                     0.0s
 => [php internal] load build definition from Dockerfile.php                                                         0.0s
 => => transferring dockerfile: 281B                                                                                 0.0s
 => WARN: FromAsCasing: 'as' and 'FROM' keywords' casing do not match (line 8)                                       0.0s
 => WARN: InvalidDefaultArgInFrom: Default value for ARG ${CLI_IMAGE} results in empty or invalid base image name (  0.0s
 => [nginx internal] load build definition from Dockerfile.nginx-drupal                                              0.0s
 => => transferring dockerfile: 384B                                                                                 0.0s
 => WARN: FromAsCasing: 'as' and 'FROM' keywords' casing do not match (line 8)                                       0.0s
 => WARN: InvalidDefaultArgInFrom: Default value for ARG ${CLI_IMAGE} results in empty or invalid base image name (  0.0s
 => [test internal] load build definition from Dockerfile.test                                                       0.0s
 => => transferring dockerfile: 323B                                                                                 0.0s
 => WARN: FromAsCasing: 'as' and 'FROM' keywords' casing do not match (line 8)                                       0.0s
 => WARN: InvalidDefaultArgInFrom: Default value for ARG ${CLI_IMAGE} results in empty or invalid base image name (  0.0s
 => [php internal] load metadata for docker.io/govcms/php:10.x-latest                                                1.4s
 => [nginx internal] load metadata for docker.io/library/pwss-paas:latest                                            0.0s
 => [test internal] load metadata for docker.io/govcms/test:10.x-latest                                              1.4s
 => [nginx internal] load metadata for docker.io/govcms/nginx-drupal:10.x-latest                                     1.4s
 => [php auth] govcms/php:pull token for registry-1.docker.io                                                        0.0s
 => [test auth] govcms/test:pull token for registry-1.docker.io                                                      0.0s
 => [nginx auth] govcms/nginx-drupal:pull token for registry-1.docker.io                                             0.0s
 => [php internal] load .dockerignore                                                                                0.0s
 => => transferring context: 275B                                                                                    0.0s
 => [nginx internal] load .dockerignore                                                                              0.0s
 => => transferring context: 275B                                                                                    0.0s
 => [test internal] load .dockerignore                                                                               0.0s
 => => transferring context: 275B                                                                                    0.0s
 => [test cli 1/1] FROM docker.io/library/pwss-paas:latest                                                           0.0s
 => [nginx stage-1 1/3] FROM docker.io/govcms/nginx-drupal:10.x-latest@sha256:ec9101ed074cec71e8ef4fc26b8486c5f655f  0.0s
 => [nginx internal] load build context                                                                              0.3s
 => => transferring context: 84B                                                                                     0.3s
 => [php stage-1 1/2] FROM docker.io/govcms/php:10.x-latest@sha256:d5e20995753b266c53314d4fb9206cc95370301681d65f32  0.0s
 => CACHED [php stage-1 2/2] COPY --from=cli /app /app                                                               0.0s
 => [php] exporting to image                                                                                         0.0s
 => => exporting layers                                                                                              0.0s
 => => writing image sha256:7d3bd5cc5e96611ac4665c6d8547c166a748240c10076b55f6d8d09b84b5dcbc                         0.0s
 => => naming to docker.io/library/govcms-pwss-paas-php                                                              0.0s
 => [test stage-1 1/3] FROM docker.io/govcms/test:10.x-latest@sha256:548a9382586e6c59b8a9b3c57c71e9cf9eb2e074e69b35  0.0s
 => [test internal] load build context                                                                               0.0s
 => => transferring context: 1.74kB                                                                                  0.0s
 => CACHED [test stage-1 2/3] COPY --from=cli /app /app                                                              0.0s
 => CACHED [test stage-1 3/3] COPY tests /app/tests/                                                                 0.0s
 => [test] exporting to image                                                                                        0.0s
 => => exporting layers                                                                                              0.0s
 => => writing image sha256:b4df98b1353016f00a24a4e39cd9cc3b9758d53b724978a323f54e28c895f8eb                         0.0s
 => => naming to docker.io/library/govcms-pwss-paas-test                                                             0.0s
 => [php] resolving provenance for metadata file                                                                     0.0s
 => [test] resolving provenance for metadata file                                                                    0.0s
 => CACHED [nginx stage-1 2/3] COPY --from=cli /app/web /app/web                                                     0.0s
 => CACHED [nginx stage-1 3/3] COPY redirects-map.conf /etc/nginx/govcms-redirects-map.conf                          0.0s
 => [nginx] exporting to image                                                                                       0.0s
 => => exporting layers                                                                                              0.0s
 => => writing image sha256:0dbfd67008fd6a5f41b6a8d3412e7c7ef2a066213d2fbf7950358b9daadb4f37                         0.0s
 => => naming to docker.io/library/govcms-pwss-paas-nginx                                                            0.0s
 => [nginx] resolving provenance for metadata file                                                                   0.0s
[+] Running 7/0
 ✔ Container govcms-pwss-paas-av-1       Running                                                                     0.0s
 ✔ Container pwss-paas                   Running                                                                     0.0s
 ✔ Container govcms-pwss-paas-mariadb-1  Running                                                                     0.0s
 ✔ Container govcms-pwss-paas-nginx-1    Running                                                                     0.0s
 ✔ Container govcms-pwss-paas-test-1     Running                                                                     0.0s
 ✔ Container govcms-pwss-paas-php-1      Running                                                                     0.0s
 ✔ Container govcms-pwss-paas-chrome-1   Running                                                                     0.0s
2024/09/10 04:34:30 Waiting for: tcp://mariadb:3306
2024/09/10 04:34:30 Connected to tcp://mariadb:3306
GovCMS Deploy :: Update Database
[info]: Rebuilding cache before database updates.
 [success] Cache rebuild complete.
[info]: Preparing database update.
 [success] No pending updates.
[success]: Completed successfully.
GovCMS Deploy :: Configuration import
[skip]: There is no configuration.
GovCMS Deploy :: Cache rebuild
 [success] Cache rebuild complete.
[success]: Completed successfully.
GovCMS Deploy :: Enable modules
[success]: Completed successfully.
Project                  :  pwss-paas
Site local URL           :  http://pwss-paas.docker.amazee.io
DB port on host          :  64338
```



## Resolution Approach ctd

Some times you might still encounter the problem even with the change daemon configuration, to attempt to solve it, you can try changing the docker configuration file at `~/.docker/config.json`:

-   **Approach-1**: by changing `"credsStore": "osxkeychain"` to `"credsStore": "desktop"`
-   **Approach-2**: by deleting the ``~/.docker/config.json`` completedly (make sure you have a backup !)

