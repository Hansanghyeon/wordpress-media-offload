<p align="center">
<img src="https://user-images.githubusercontent.com/42893446/192394703-9084093c-91a7-4121-b2b5-6f39edb8bbad.jpg" width="368px">
</p>


<h2 align="center">Welcome π</h2>

> Wordpress & media offload & minio template (docker)

- [Blog Tool, Publishing Platform, and CMS | WordPress.org νκ΅­μ΄](https://ko.wordpress.org/)
- [Upload Your WordPress Media to Amazon S3 with WP Offload Media - Delicious Brains Inc](https://deliciousbrains.com/wp-offload-media/)
- [MinIO | High Performance, Kubernetes Native Object Storage](https://min.io/)

## folder structure

```
.
βββ .docker
β   βββ db
β   β   βββ data              // mariadbμ λ°μ΄ν° ν΄λ
β   β   βββ .gitkeep
β   βββ minio                 // S3 open source
β   βββ wp                    // wordpress:/var/www/html
β       βββ wp-content        // μλνλ μ€ μ»¨νμΈ  ν΄λ
β       βββ .gitkeep
βββ .env.example
βββ .gitignore
βββ Makefile
βββ README.md
βββ apps
β   βββ theme                 // μλνλ μ€μμ μ¬μ©ν  νλ§ ν΄λ
β       βββ .gitkeep
βββ docker-compose.yaml
```

## offload media μ μ©νκΈ°

```php
// functions
<?php

function minio_s3_client_args( $args ) {
    $args['endpoint'] = 'http://minio:9000';
    $args['use_path_style_endpoint'] = true;
    return $args;
}
add_filter( 'as3cf_aws_s3_client_args', 'minio_s3_client_args' );

add_filter( 'as3cf_aws_s3_url_domain', 'minio_s3_url_domain', 10, 2 );
function minio_s3_url_domain( $domain, $bucket ) {
    return getenv_docker('CDN_DOMAIN', '{{default domain}}').'/' . $bucket;
}
```

```sh
docker-compose up -d
```

## Author

π€ **Hansanghyeon**

* Website: [hyeon.pro](https://hyeon.pro)
* Github: [@Hansanghyeon](https://github.com/Hansanghyeon)
