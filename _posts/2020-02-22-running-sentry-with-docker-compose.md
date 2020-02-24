---
layout: post
tags: [sentry, build, blog]
image: '/images/posts/2020-02-23-sentry-ui.png'
---

You can use docker to  run sentry  on a unix-based system using `docker compose`. I will be following the steps in this [documentation](https://docs.sentry.io/server/installation/) for the build.

+ ```bash
  git clone https://github.com/getsentry/onpremise.git
  ```

+ ```bash
  cd onpremise && ./install.sh
  ```

  You should get something similar to the log

```bash
...
Creating sentry_onpremise_snuba-replacer_1 ... done
Creating sentry_onpremise_snuba-consumer_1 ... done
Creating sentry_onpremise_snuba-api_1      ... done
Creating sentry_onpremise_postgres_1       ... done
01:53:38 [WARNING] sentry.utils.geo: settings.GEOIP_PATH_MMDB not configured.
01:53:44 [INFO] sentry.plugins.github: apps-not-configured
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

+ ```bash
  docker-compose up -d
  ```

  

Just like the previous step, you should get something like this below;

```bash
$ docker-compose up -d
Starting sentry_onpremise_redis_1                ... done
Starting sentry_onpremise_postgres_1             ... done
Starting sentry_onpremise_smtp_1                 ... done
Starting sentry_onpremise_zookeeper_1            ... done
Starting sentry_onpremise_symbolicator_1         ... done
Starting sentry_onpremise_clickhouse_1           ... done
Starting sentry_onpremise_memcached_1            ... done
Creating sentry_onpremise_symbolicator-cleanup_1 ... done
Starting sentry_onpremise_kafka_1                ... done
Starting sentry_onpremise_snuba-replacer_1       ... done
Starting sentry_onpremise_snuba-api_1            ... done
Starting sentry_onpremise_snuba-consumer_1       ... done
Creating sentry_onpremise_snuba-cleanup_1          ... done
Creating sentry_onpremise_web_1                    ... done
Creating sentry_onpremise_cron_1                   ... done
Creating sentry_onpremise_worker_1                 ... done
Creating sentry_onpremise_post-process-forwarder_1 ... done
Creating sentry_onpremise_sentry-cleanup_1         ... done
```



You should now be able to access sentry at [http://localhost:9000/](http://localhost:9000/) . If you run into connection issues, you can try again. 