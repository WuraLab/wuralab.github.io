---
layout: post
author: 'Tunde Oladipupo'
tags: [sentry, development, blog]

---

 If you follow our previous blog [post](./2020-02-22-running-sentry-with-docker-compose.md), you will see how to run sentry locally but using latest getsentry/sentry:latest docker image. In this tutorial, I will be working through how to develop sentry locally using docker and docker-compose;

+ Make all your  local changes .

+ Once ready, build a new docker image with your changes.

  ```bash
  $docker build -t sentry-local:latest -f docker/Dockerfile  .
  ...
  Removing intermediate container acd425ce0e97
   ---> bf50a8650c25
  Step 48/49 : LABEL org.opencontainers.image.revision=$SOURCE_COMMIT
   ---> Running in 290f5fc2f77f
  Removing intermediate container 290f5fc2f77f
   ---> 8ee312b84967
  Step 49/49 : LABEL org.opencontainers.image.licenses="https://github.com/getsentry/sentry/blob/${SOURCE_COMMIT:-master}/LICENSE"
   ---> Running in 1ddf8d923af2
  Removing intermediate container 1ddf8d923af2
   ---> cbbe1b918f07
  Successfully built cbbe1b918f07
  Successfully tagged sentry-local:latest
  ```

  

+ Once image is properly built, run sentry locally using [sentry/onpremise](https://github.com/getsentry/onpremise) repo.

+ In the `onpremise` repo, remove this [line](https://github.com/getsentry/onpremise/blob/master/install.sh#L109) that pulls sentry  from dockerhub  from your local repo.

+ Once that line has been removed, build sentry-onprem docker image.

  ```bash 
  
  $cd onpremise/
  $SENTRY_IMAGE=sentry-local:latest  ./install.sh
  ...
  Creating sentry_onpremise_snuba-consumer_1          ... done
  15:35:42 [WARNING] sentry.utils.geo: settings.GEOIP_PATH_MMDB not configured.
  15:35:46 [INFO] sentry.plugins.github: apps-not-configured
  Operations to perform:
    Apply all migrations: admin, auth, contenttypes, jira_ac, nodestore, sentry, sessions, sites, social_auth
  Running migrations:
    No migrations to apply.
  Creating missing DSNs
  Correcting Group.num_comments counter
  Cleaning up...
  
  ----------------
  You're all done! Run the following command to get Sentry running:
  
    docker-compose up -d
    
  ```

  

+ Start docker-compose to launch your local sentry.

  ```bash
   $docker-compose up -d
   Starting sentry_onpremise_snuba-consumer_1          ... done
  Starting sentry_onpremise_snuba-outcomes-consumer_1 ... done
  Starting sentry_onpremise_snuba-replacer_1          ... done
  Creating sentry_onpremise_snuba-cleanup_1           ... done
  Creating sentry_onpremise_worker_1                  ... done
  Creating sentry_onpremise_cron_1                    ... done
  Creating sentry_onpremise_web_1                     ... done
  Creating sentry_onpremise_post-process-forwarder_1  ... done
  Creating sentry_onpremise_sentry-cleanup_1          ... done
  ```

  

  You should now be able to see your local development changes at http://localhost:9000/auth/login/sentry/

  



