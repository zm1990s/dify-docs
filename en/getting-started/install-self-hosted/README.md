# Dify Community

Dify, an open-source project on [GitHub](https://github.com/langgenius/dify), can be self-hosted using either of these methods:

1. [Docker Compose Deployment](https://docs.dify.ai/getting-started/install-self-hosted/docker-compose)
2. [Local Source Code Start](https://docs.dify.ai/getting-started/install-self-hosted/local-source-code)

### Contributing

To maintain code quality, we require all code contributions - even from those with direct commit access - to be submitted as pull requests. These must be reviewed and approved by the core development team before merging.

We welcome contributions from everyone! If you're interested in helping, please check our [Contribution Guide](https://github.com/langgenius/dify/blob/main/CONTRIBUTING.md) for more information on getting started.

### High frequency questions

#### How to reset the password of the admin account?

If you deployed using Docker Compose, you can reset the password with the following command while your Docker Compose is running:

```
docker exec -it docker-api-1 flask reset-password
```

It will prompt you to enter the email address and the new password. Example:

```
dify@my-pc:~/hello/dify/docker$ docker compose up -d
[+] Running 9/9
 ✔ Container docker-web-1         Started                                                              0.1s 
 ✔ Container docker-sandbox-1     Started                                                              0.1s 
 ✔ Container docker-db-1          Started                                                              0.1s 
 ✔ Container docker-redis-1       Started                                                              0.1s 
 ✔ Container docker-weaviate-1    Started                                                              0.1s 
 ✔ Container docker-ssrf_proxy-1  Started                                                              0.1s 
 ✔ Container docker-api-1         Started                                                              0.1s 
 ✔ Container docker-worker-1      Started                                                              0.1s 
 ✔ Container docker-nginx-1       Started                                                              0.1s 
dify@my-pc:~/hello/dify/docker$ docker exec -it docker-api-1 flask reset-password
None of PyTorch, TensorFlow >= 2.0, or Flax have been found. Models won't be available and only tokenizers, configuration and file/data utilities can be used.
sagemaker.config INFO - Not applying SDK defaults from location: /etc/xdg/sagemaker/config.yaml
sagemaker.config INFO - Not applying SDK defaults from location: /root/.config/sagemaker/config.yaml
Email: hello@dify.ai
New password: newpassword4567
Password confirm: newpassword4567
Password reset successfully.
```

View more [FAQs](https://docs.dify.ai/getting-started/install-self-hosted/faqs)

[FAQs](https://docs.dify.ai/learn-more/faq/install-faq).
